# Java文件的读写

## 字节输入输出流复制文件
```
public static void main(String[] args) {
    long s = System.currentTimeMillis();
    FileInputStream fis = null;
    FileOutputStream fos = null;
    try{
        fis = new FileInputStream("c:\\t.zip");
        fos = new FileOutputStream("d:\\t.zip");
        //定义字节数组,缓冲
        byte[] bytes = new byte[1024*10];
        //读取数组,写入数组
        int len = 0 ; 
		while((len = fis.read(bytes))!=-1){
			fos.write(bytes, 0, len);
		}
	}catch(IOException ex){
		System.out.println(ex);
		throw new RuntimeException("文件复制失败");
	}finally{
		try{
			if(fos!=null)
				fos.close();
		}catch(IOException ex){
			throw new RuntimeException("释放资源失败");
		}finally{
			try{
				if(fis!=null)
					fis.close();
			}catch(IOException ex){
				throw new RuntimeException("释放资源失败");
			}
		}
	}
}
```

## buffered缓冲流高效文件复制代码
```
public static void copy_4(File src,File desc)throws IOException{
	BufferedInputStream bis = new BufferedInputStream(new FileInputStream(src));
	BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(desc));
	int len = 0 ;
	byte[] bytes = new byte[1024];
	while((len = bis.read(bytes))!=-1){
		bos.write(bytes,0,len);
	}
	bos.close();
	bis.close();
}
```
