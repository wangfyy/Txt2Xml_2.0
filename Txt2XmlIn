import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

/*
将Excel报文的前7列复制到txt2Xml目录下分别以交易代码命名的txt文件，
可以是多个，例如同时新建1301.txt和1302.txt，运行代码，
在1301和1302交易目录(注意修改路径)下生成1301.msgin和1302.msgin。
注意：txt2XmlIn文件下不要有其他文件或文件夹
*/

public class Txt2XmlIn {
	public static void readTxtFile(String filePath1, String fileName, String filePath2) {
		try {
			/*FileReader reader = new FileReader(filePath1);
			FileWriter writer = new FileWriter(filePath2, true);*/
			/*转换流*/
			String encoding = "GBK";
			File file1 = new File(filePath1);
			File file2 = new File(filePath2);
			InputStreamReader reader = new InputStreamReader(new FileInputStream(file1), encoding);
			OutputStreamWriter writer = new OutputStreamWriter(new FileOutputStream(file2), encoding);
			BufferedReader br = new BufferedReader(reader);
			BufferedWriter bw = new BufferedWriter(writer);
			String lineTxt;
			StringBuilder content1 = new StringBuilder("");
			content1.append(
					"<?xml version=\"1.0\" encoding=\"gb2312\" ?>" + "\n" +
					"<msg>" + "\n" +
					"<basic-info>" + "\n" +
					"<name>"+fileName+".msgin</name>" + "\n" +
							"<author></author>" + "\n" +
							"<date></date>" + "\n" +
							"<modifier></modifier>" + "\n" +
							"<modifyDate></modifyDate>" + "\n" +
							"<type>IN</type>" + "\n" +
							"<desc>"+fileName+".msgin</desc>" + "\n" +
									"<event_class_name></event_class_name>" + "\n" +
									"<protocal>TCP</protocal>" + "\n" +
									"</basic-info>" + "\n" +
									"<msg-content>" + 
									"\n");
			bw.write(content1.toString());
			while ((lineTxt = br.readLine()) != null) {
				String[] result = getXMLcode(lineTxt);
				StringBuilder content = new StringBuilder("");
				if (result[2] == null)
					content.append(
								"<var namespace=\"\" expr=\"" 
								+ result[1] 
								+ "\" desc=\"\" lentype=\"VARLEN\" len=\"" 
								+ result[6]
								+ "\" loc=\"\" align=\"LEFT\" fill=\"#20\" compart=\"\" class=\"\" handleprocess=\"\" argvar=\"\" mac=\"\" />"
								+ "\n"
								);
				else
					content.append(
								"<var namespace=\"\" expr=\"" 
								+ result[1] 
								+ "\" desc=\"" 
								+ result[2]
								+ "\" lentype=\"VARLEN\" len=\"" 
								+ result[6]
								+ "\" loc=\"\" align=\"LEFT\" fill=\"#20\" compart=\"\" class=\"\" handleprocess=\"\" argvar=\"\" mac=\"\" />"
								+ "\n"
								);
				bw.write(content.toString());
			}
			StringBuilder content2 = new StringBuilder("");
			content2.append(
					"</msg-content>" +
					"</msg>"
					);
			bw.write(content2.toString());
			br.close();
			bw.close();
		} catch (Exception e) {
			System.out.println("读取文件内容出错");
			e.printStackTrace();
		}
	}

	public static String[] getXMLcode(String str) {
		String[] result = new String[7];
		int st = 0, index = 0;
		for (int i = 0; i < str.length(); i++) {
			if (str.charAt(i) == '\t' || i == str.length() - 1) {
				if (i == str.length() - 1)
					result[index++] = str.substring(st, i + 1);
				else
					result[index++] = str.substring(st, i);
				st = i + 1;
			}
		}
		return result;
	}

	// 获取不带后缀名的文件名
	public static String getFileNameWithoutSuffix(String file_name) {
		return file_name.substring(0, file_name.lastIndexOf("."));
	}

	public static void main(String[] args) {
		/* txt文件目录 */
		String fileDirectory1 = "C:/Users/wasdw/Desktop/txt2XmlIn/";
		File file = new File(fileDirectory1);
		if (!file.isDirectory()) {
			System.out.println("目录不存在");
			return;
		}
		String[] fileName = file.list();
		for (String perFileName : fileName) {
			System.out.println("读取 " + getFileNameWithoutSuffix(perFileName) + " msgin型交易报文数据...");
			/* xml文件目录 */
			String fileDirectory2 = 
				"C:/Users/wasdw/desktop/nantian/ABSIDE/workspace/ABS50_DEMO工程/abs01/com/nantian/abs40/transaction/yibentong/T" + getFileNameWithoutSuffix(perFileName) + "/";
			readTxtFile(
						fileDirectory1 + perFileName, 
						getFileNameWithoutSuffix(perFileName) ,
						fileDirectory2 + "/" + getFileNameWithoutSuffix(perFileName)
						+ ".msgin");
			System.out.println("在 " + fileDirectory2 + " 下生成 "+ getFileNameWithoutSuffix(perFileName) + ".msgin 报文文件");
		}
	}
}
