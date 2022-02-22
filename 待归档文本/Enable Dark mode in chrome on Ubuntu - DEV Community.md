> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [dev.to](https://dev.to/ankitbrijwasi/enable-dark-mode-in-chrome-on-ubuntu-20na)

> Recently I started using Ubuntu as my default OS for programming and I am loving working in it! But.......

[![](https://res.cloudinary.com/practicaldev/image/fetch/s--Fp9negTk--/c_fill,f_auto,fl_progressive,h_50,q_auto,w_50/https://dev-to-uploads.s3.amazonaws.com/uploads/user/profile_image/353210/1c03d3af-6092-430e-9434-9bed2aa0d9da.jpeg)](https://dev.to/ankitbrijwasi)

Recently I started using Ubuntu as my default OS for programming and I am loving working in it!

But there was an issue which I faced, By default in Google Chrome dark mode is not enabled and it was kind of a letdown.

After digging up the Internet I found that In order to enable the Dark mode I needed to edit the `google-chrome.desktop` file.

If you are also dealing with a similar issue then, just follow along

Firstly open, the `google-chrome.desktop` file using,  
`sudo gedit /usr/share/applications/google-chrome.desktop`

After the file has been opened, you will need to edit two lines

1. Search for the line-  

```
Exec=/usr/bin/google-chrome-stable %U


```

replace it with-  

```
Exec=/usr/bin/google-chrome-stable %U --enable-features=WebUIDarkMode --force-dark-mode


```

2. Search for the line-  

```
Exec=/usr/bin/google-chrome-stable


```

replace it with-  

```
Exec=/usr/bin/google-chrome-stable --enable-features=WebUIDarkMode --force-dark-mode


```

Now, Save the file and restart Chrome. Dark mode should be enabled now

Thanks for reading!  
Have a nice day!😇