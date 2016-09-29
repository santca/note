# io流
===================

* 流的概念
	
	* 流是一组有顺序的，有起点和终点的字节集合，是对数据传输的总称或抽象。
	
	* 所谓的IO就是指流的读(input输入)与写(output输出)操作的简称。
	
	* Java对数据的操作是通过流的方式
	
    * IO流用来处理设备之间的数据传输
	
    * 注意：Java用于操作流的对象都在IO包中
	
* 流的分类
   
    * 根据数据流向不同分为： 程序中需要根据待传输数据的不同特性而使用不同的流
	
		1. 输入流（intput）对输入流只能进行读操作
		
		2. 输出流（output），对输出流只能进行写操作 
		
	* 根据处理数据类型的不同分为：字节流和字符流
	
		1. 字节流 ：InputStream是所有字节输入流的祖先，而OutputStream是所有字节输出流的祖先。
		
		2. 字符流： Reader是所有读取字符串输入流的祖先，而Writer是所有输出字符串的祖先。
		
		3. 字节流和字符流的操作都是采用如下的步骤完成： 
		
			1. 找到一个要操作的资源，可能是文件，可能是其他的位置 
			
			2. 根据字节流或字符流的子类，决定输入及输出的位置 
			
			3. 进行读或写的操作 
			
			4. 关闭 


* File类

	在File类中包含了大部分和文件操作的功能方法，
	该类的对象可以代表一个具体的文件或文件夹，
	所以以前曾有人建议将该类的类名修改成FilePath，
	因为该类也可以代表一个文件夹，更准确的说是可以代表一个文件路径。
	
	* 创建文件夹
	
		package com;

		import java.io.File;

		/**
		 * Created by chenyan on 2016/9/29.
		 */
		public class FileDemo {

			public static void main(String[] args) {

				// 创建一个File对象
				File file = new File("E:\\tmp\\安卓6组\\java部分");

				// 创建文件夹
				// 要判断文件夹存在与否 不存在再创建文件夹
				if (!file.exists()) {
					file.mkdirs();
				}

			}
		}
		
	* 创建文件
	
		package com;

		import java.io.File;
		import java.io.IOException;

		/**
		 * Created by chenyan on 2016/9/29.
		 */
		public class FileDemo {

			public static void main(String[] args) {

				// 创建一个File对象
				File file = new File("E:\\tmp\\测试");

				file.mkdirs();

				// 根据文件所在文件夹对象，创建文件
				File fileDoc = new File("E:\\tmp\\测试","爱国.doc");

				// 创建文件
				try {
					fileDoc.createNewFile();
				} catch (IOException e) {
					e.printStackTrace();
				}

			}
		}
		
	* 判断File对象是目录还是文件
	
	package com;

	import java.io.File;
	import java.io.IOException;

	/**
	 * Created by chenyan on 2016/9/29.
	 */
	public class FileDemo {

		public static void main(String[] args) {

			// 创建一个File对象
			File file = new File("E:\\tmp\\测试\\爱党\\爱国.doc");

		   // 判断 file 是文件夹还是文件
			boolean bln = file.isDirectory();
			boolean bln1 = file.isFile();

			System.out.println("是否是目录："+bln+"|是否是文件:"+bln1);

		}
	}

	* 给文件重命名
	
	package com;

	import java.io.File;
	import java.io.IOException;

	/**
	 * Created by chenyan on 2016/9/29.
	 */
	public class FileDemo {

		public static void main(String[] args) {

			// 创建一个File对象
			File file = new File("E:\\tmp\\测试\\爱国.doc");
			try {
				file.createNewFile();
			} catch (IOException e) {
				e.printStackTrace();
			}
			// 判断 file 是文件夹还是文件
			boolean bln = file.isDirectory();
			boolean bln1 = file.isFile();

			// 所谓的修改文件的名称，实际上是先把源文件内容复制到一个新名称的新文件中，
			// 然后把源文件给删除
			file.renameTo(new File("E:\\tmp\\测试\\","不爱国.doc"));

			// 获取file的名字
			System.out.println("文件的（绝对）路径:" + file.getAbsolutePath());
			System.out.println("文件的名字:" + file.getName());
			System.out.println("是否是目录：" + bln + "|是否是文件:" + bln1);

		}
	}
	
	* 修改文件夹
	
	package com;

	import java.io.File;
	import java.io.IOException;

	/**
	 * Created by chenyan on 2016/9/29.
	 */
	public class FileDemo {

		public static void main(String[] args) {

			// 创建一个File对象
			File file = new File("E:\\tmp\\测试");

			// 判断 file 是文件夹还是文件
			boolean bln = file.isDirectory();
			boolean bln1 = file.isFile();

			// 修改文件夹是将文件夹改名
			file.renameTo(new File("E:\\tmp\\测试1"));

			// 获取file的名字
			System.out.println("文件的（绝对）路径:" + file.getAbsolutePath());
			System.out.println("文件的名字:" + file.getName());
			System.out.println("是否是目录：" + bln + "|是否是文件:" + bln1);

		}
	}
	
	* 列出指定文件夹下的所有文件和文件夹(包括子文件夹)
	
		package com;

		import java.io.File;

	
		public class FileDemo {

			public static void main(String[] args) {

				// 创建一个File对象
				File file = new File("e:\\tmp\\测试1");
				
				testFile(file);
				/*
				// 列出file文件及所有子文件夹下的所有的文件的名字
				String[] strNames = file.list();

				for (String fileName:strNames) {
					File tmpFile = new File(file.getAbsolutePath(),fileName);

					// 判断是否为目录，如果是目录的话，那么就去看看它下面有没有文件，有文件的话，就
					// 列出来，没有的话就不用列出来
					if (!tmpFile.isFile()) {
						String[] strNames1 = tmpFile.list();
						if(strNames1 != null && strNames1.length > 0) {
							for (String fileName1:strNames1) {
								System.out.println(fileName1);
							}
						}
					}
					System.out.println(fileName+"是否为文件"+tmpFile.isFile());
				}*/
			}

			public static void testFile(File file) {
				// 判断file是文件还是文件夹
				// 如果是文件的话

				System.out.println(file.getName());

				if (file.isFile()) {
					//System.out.println(file.getName());
				}

				if (file.isDirectory()) {
					//System.out.println(file);

					File[] strNames = file.listFiles();
					if (strNames !=null && strNames.length > 0) {
						for (File fileName:strNames) {
						  

							testFile(fileName);
						}
					}

				}
			}
		}
		
	* 复制文件
	
		package com;

		import java.io.*;

		/**
		 * Created by chenyan on 2016/9/29.
		 */
		public class IODemo {

			public static void main(String[] args) {

				// 复制文件
				// 把本地e:\\tmp\\sources\\source_file.txt文件
				// 复制到e:\\tmp\\target\\target_file.md文件中

				String s1 = "e:\\tmp\\sources\\source_file.txt";
				String s2 = "e:\\tmp\\target";
				String s3 = "target_file.txt";

				copyFileCharBuffer(s1, s2, s3);
			}

			/**
			 * 复制文件字节流版本
			 *
			 * @param sourceFileName 源文件路径+名称 例如： e:\tmp\sources\source_file.txt
			 * @param targetFilePath 目标路径 例如：e:\tmp\target
			 * @param targerFileName 目标文件 例如： target_file.md
			 */
			public static void copyFileByte(String sourceFileName, String targetFilePath, String targerFileName) {
				 /*
				1. 找到一个要操作的资源，可能是文件，可能是其他的位置

				2. 根据字节流或字符流的子类，决定输入及输出的位置

				3. 进行读或写的操作

				4. 关闭
				*/

				// 字节流版本
				// 复制的原理
				// 1.确认源文件的位置
				File sourceFile = new File(sourceFileName);

				// 2.建立目标目录和空的目标文件
				File targetDic = new File(targetFilePath);

				if (!targetDic.exists()) {
					targetDic.mkdirs();
				}

				File targetFile = new File(targetDic, targerFileName);

				try {
					if (!targetFile.exists()) {
						targetFile.createNewFile();
					}

					// 3.把源文件的内容加载到输入流中

					// 创建输入流对象
					InputStream is = new FileInputStream(sourceFile);

					// 创建输出流对象
					OutputStream os = new FileOutputStream(targetFile);

					// 4.使用输出流把输入流的内容写到目标文件中
					int tmp = 0;
					while ((tmp = is.read()) != -1) {
						os.write(tmp);
					}

					// 关闭流
					os.flush();
					os.close();
					is.close();
				} catch (IOException e) {
					e.printStackTrace();
				}


			}

			/**
			 * 复制文件字符流版本
			 *
			 * @param sourceFileName 源文件路径+名称 例如： e:\tmp\sources\source_file.txt
			 * @param targetFilePath 目标路径 例如：e:\tmp\target
			 * @param targerFileName 目标文件 例如： target_file.md
			 */
			public static void copyFileChar(String sourceFileName, String targetFilePath, String targerFileName) {
				 /*
				1. 找到一个要操作的资源，可能是文件，可能是其他的位置

				2. 根据字节流或字符流的子类，决定输入及输出的位置

				3. 进行读或写的操作

				4. 关闭
				*/

				// 字符流版本
				// 复制的原理
				// 1.确认源文件的位置
				File sourceFile = new File(sourceFileName);

				// 2.建立目标目录和空的目标文件
				File targetDic = new File(targetFilePath);

				if (!targetDic.exists()) {
					targetDic.mkdirs();
				}

				File targetFile = new File(targetDic, targerFileName);

				try {
					if (!targetFile.exists()) {
						targetFile.createNewFile();
					}

					// 3.把源文件的内容加载到输入流中

					// 创建输入流对象
					InputStreamReader is = new InputStreamReader(new FileInputStream(sourceFileName), "GBK");

					// 创建输出流对象
					OutputStreamWriter os = new OutputStreamWriter(new FileOutputStream(targetFile), "GBK");

					// 4.使用输出流把输入流的内容写到目标文件中
					int tmp = 0;
					while ((tmp = is.read()) != -1) {
						char c = (char) tmp;

						os.write(String.valueOf(c).toCharArray());
					}

					// 关闭流
					os.flush();
					os.close();
					is.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}

			public static void copyFileCharBuffer(String sourceFileName, String targetFilePath, String targerFileName) {
				/*
				1. 找到一个要操作的资源，可能是文件，可能是其他的位置

				2. 根据字节流或字符流的子类，决定输入及输出的位置

				3. 进行读或写的操作

				4. 关闭
				*/

				// 字符流版本
				// 复制的原理
				// 1.确认源文件的位置
				File sourceFile = new File(sourceFileName);

				// 2.建立目标目录和空的目标文件
				File targetDic = new File(targetFilePath);

				if (!targetDic.exists()) {
					targetDic.mkdirs();
				}

				File targetFile = new File(targetDic, targerFileName);

				try {
					if (!targetFile.exists()) {
						targetFile.createNewFile();
					}

					// 3.把源文件的内容加载到输入流中

					// 创建输入流对象
					BufferedReader is = new BufferedReader(new FileReader(sourceFileName));

					// 创建输出流对象
					BufferedWriter os = new BufferedWriter(new FileWriter(targetFile));

					// 4.使用输出流把输入流的内容写到目标文件中
					String strLine = "";
					while (true) {

						if (strLine == null) {
							break;
						}

						strLine = is.readLine();

						if (strLine != null) {

							strLine = new String(strLine.getBytes(), "utf-8");

							System.out.println(strLine);
							os.write(strLine);
						}


					}

					// 关闭流
					os.flush();
					os.close();
					is.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}








