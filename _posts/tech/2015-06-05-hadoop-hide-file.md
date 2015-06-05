---
layout: post
title: Hdfs隐藏文件设置
city: 北京
tags: [tech,hadoop,hole]
---

Hadoop 隐藏文件设置
============

+ 按照常理来说，我不会认为hadoop上有隐藏文件，只会有权限这样设置，但是当我真的走过这个坑的时候，深深寒意，提醒我，tm我不知道啊
+ Hadoop Mapreduce，设置的文件过滤器，会自动过滤掉 "_" "." 两个标点开头的文件
+ 例如：/xx/_a hadoop fs list /xx/ 是能看见_a，但是mapreduce作为输入是不能看见的
+ 没图没真相，贴代码；


:::
    
    private long minSplitSize = 1;
    //一个隐藏文件实现，过滤开头为_ 和. 文件过滤器
    private static final PathFilter hiddenFileFilter = new PathFilter(){
      public boolean accept(Path p){
        String name = p.getName(); 
        return !name.startsWith("_") && !name.startsWith("."); 
      }
    };
    //获取文件
    protected FileStatus[] listStatus(JobConf job) throws IOException {
        Path[] dirs = getInputPaths(job);
        if (dirs.length == 0) {
            throw new IOException("No input paths specified in job");
        }
        // get tokens for all the required FileSystems..
        TokenCache.obtainTokensForNamenodes(job.getCredentials(), dirs, job);
    
        // Whether we need to recursive look into the directory structure
        boolean recursive = job.getBoolean(INPUT_DIR_RECURSIVE, false);
        // creates a MultiPathFilter with the hiddenFileFilter and the
        // user provided one (if any).
        List<PathFilter> filters = new ArrayList<PathFilter>();
        filters.add(hiddenFileFilter); //田间隐藏文件过滤器
        PathFilter jobFilter = getInputPathFilter(job); //获得设置隐藏文件过滤器
        if (jobFilter != null) {
            filters.add(jobFilter);
        }
        PathFilter inputFilter = new MultiPathFilter(filters); //常见多重过滤器
        FileStatus[] result;
        int numThreads = job
            .getInt(
                org.apache.hadoop.mapreduce.lib.input.FileInputFormat.LIST_STATUS_NUM_THREADS,
                org.apache.hadoop.mapreduce.lib.input.FileInputFormat.DEFAULT_LIST_STATUS_NUM_THREADS);
    
        StopWatch sw = new StopWatch().start();
        if (numThreads == 1) {
            List<FileStatus> locatedFiles = singleThreadedListStatus(job, dirs, inputFilter, recursive); 
            result = locatedFiles.toArray(new FileStatus[locatedFiles.size()]);
        } else {
            Iterable<FileStatus> locatedFiles = null;
        try {
        
            LocatedFileStatusFetcher locatedFileStatusFetcher = new LocatedFileStatusFetcher(
            job, dirs, recursive, inputFilter, false);
            locatedFiles = locatedFileStatusFetcher.getFileStatuses();
        } catch (InterruptedException e) {
            throw new IOException("Interrupted while getting file statuses");
        }
        result = Iterables.toArray(locatedFiles, FileStatus.class);
        }
        sw.stop();
        if (LOG.isDebugEnabled()) {
            LOG.debug("Time taken to get FileStatuses: "
            + sw.now(TimeUnit.MILLISECONDS));
        }
        LOG.info("Total input paths to process : " + result.length);
        return result;
    } 


