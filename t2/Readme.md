
# 猜数字
t2是一个猜数字的练习。
1.涉及到随机数的使用方法
2.涉及到键盘输入的使用方法
3.涉及到资源关闭的使用方法
4.因为IO流需要关闭资源（虽然本例中不关闭也可以），所以t_1使用try，finally的方法进行资源关闭尝试，但是报错Exception in thread "main" java.util.NoSuchElementException。
5.寻找方法后t_2里面将close放在了for循环的外面，错误原因大概是因为每次循环都关闭一次资源导致的错误。
