利用matlab确定图像中圆形的圆心的问题，因为这个和我后续的想法有关系，这是最近整个工作的第一步。
首先找到一段matlab的可以处理圆心的代码(当然没有自己写，因为自己实力不允许，我只是一只伪装自己的菜鸡)
运行遇到的问题：
Error using edge
Expected input number 1, I, to be two-dimensional.
Error in edge>parse_inputs (line 482)
validateattributes(I,{'numeric','logical'},{'real','nonsparse','2d'},mfilename,'I',1);
Error in edge (line 213)
[a,method,thresh,sigma,thinning,H,kx,ky] = parse_inputs(args{:});
判断edge函数数据调用出现了问题，于是决定排查调用的相关数据，通过查阅matlab论坛和相关资料。
![问题1](https://github.com/user-attachments/assets/0788014d-0e52-416e-b2c3-80c79291bf04)
判断是图像灰度处理不到位，就是说edge函数只能处理二维数据，而imbinarize处理图像产生的数据并不满足edge的要求，所以在函数中加上了判断图片灰度的代码和进一步的灰度处理代码，结果发现和自己预期一致，问题得到解决。
接下来又出现了Undefined function or variable 'Circle_Fitting'. 好的，我再次承认代码是copy来的，所以这里应该是人家直接调用了某个编写好的function，而我并没有这段代码，所以才报错undefined，于是接下来，继续找到了这段代码，但是由于这段代码太长，整个直接编进来会显得及其庞大，于是决定将它直接编写一个m文件！
做完这一切程序终于不再报错，而我并没得到最后的结果，如下图，三个及其醒目的NAN原因呢？没办法，只能随着变量一步一步向上排查，到底是哪里出现了问题，没报错也不是什么好消息呢。从xc—>para,好的应该是m文件的问题，清晰可见m代码的function只输入一个数据，而matlab命令窗口是一个矩阵，这就是问题所在了！
![问题2](https://github.com/user-attachments/assets/485e4551-3cac-4ca0-8685-b73410cfda30)