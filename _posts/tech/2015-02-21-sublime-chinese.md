---
layout: post  
title: Ubuntu sublime text 3  输入中文  
tags: [tech]   
---

Ubuntu Subime Text3 输入中文
==============

+ 保存下面的代码到文件sublime_imfix.c

        #include <gtk/gtkimcontext.h>
        void gtk_im_context_set_client_window (GtkIMContext *context,
                GdkWindow    *window)
        {
            GtkIMContextClass *klass;
            g_return_if_fail (GTK_IS_IM_CONTEXT (context));
            klass = GTK_IM_CONTEXT_GET_CLASS (context);
            if (klass->set_client_window)
            klass->set_client_window (context, window);
            g_object_set_data(G_OBJECT(context),"window",window);
            if(!GDK_IS_WINDOW (window))
                return;
            int width = gdk_window_get_width(window);
            int height = gdk_window_get_height(window);
            if(width != 0 && height !=0)
            gtk_im_context_focus_in(context);
        }
+ 将上一步的代码编译成共享库libsublime-imfix.so
    
        gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC 

+ 将libsublime-imfix.so拷贝到sublime_text所在文件夹
    
        sudo mv libsublime-imfix.so /opt/sublime_text/

+ 修改文件/usr/bin/subl的内容
    
        sudo vi /usr/bin/subl
        将   exec   /opt/sublime_text/sublime_text "$@"    替换为LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so exec /opt/sublime_text/sublime_text "$@"

+  为了使用鼠标右键打开文件时能够使用中文输入，还需要修改文件sublime_text.desktop的内容。
    
        sudo vi /usr/share/applications/sublime_text.desktop
        [Desktop Entry]
        Exec=/opt/sublime_text/sublime_text %F
        修改为
        Exec=bash -c "LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so exec /opt/sublime_text/sublime_text %F"
        将[Desktop Action Window]
        Exec=/opt/sublime_text/sublime_text -n
        修改为
        Exec=bash -c "LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so exec /opt/sublime_text/sublime_text -n"
        将[Desktop Action Document]
        Exec=/opt/sublime_text/sublime_text --command new_file
        修改为
        Exec=bash -c "LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so exec /opt/sublime_text/sublime_text --command new_file"

注意
--------------
修改时请注意双引号"",否则会导致不能打开带有空格文件名的文件。
此处仅修改了/usr/share/applications/sublime-text.desktop，但可以正常使用了。
opt/sublime_text/目录下的sublime-text.desktop可以修改，也可不修改。

参考
---------
+ [Ubuntu下Sublime Text 3解决无法输入中文的方法](http://jingyan.baidu.com/article/f3ad7d0ff8731609c3345b3b.html)      

