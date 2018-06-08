- 如果 遇到登录不进去，大概率就是session问题，
 
- 查看 tp 本身的session驱动，看他保存在哪里，大概率都是默认保存在系统缓存中
 
- 所以 这时候打印出PHP的session保存路径

- phpinfo() 查看 session.save_path 大概率是没有创建这个文件夹
 
- 创建 && 给与写权限
