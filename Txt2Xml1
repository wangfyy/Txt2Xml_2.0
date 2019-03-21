import java.io.BufferedReader;
import java.io.File;
import java.io.FileInputStream;
import java.io.InputStreamReader;
 
/**
 * Desc:
 * @describe 手动将Excel报文的前7列复制到TXT文件，运行代码在控制台复制XML
 * @author wangfy
 * @date 
 * @version 1.1
 * @param 
 * @return 
 * @throws 
 */
 
public class Txt2Xml1 {
	public static void readTxtFile(String filePath) {
		try {
			String encoding = "GBK";
			File file = new File(filePath);
			if (file.isFile() && file.exists()) {
				InputStreamReader read = new InputStreamReader(new FileInputStream(file), encoding);
				BufferedReader bufferedReader = new BufferedReader(read);
				String lineTxt = null;
				while ((lineTxt = bufferedReader.readLine()) != null) {
					String[] result = getXMLcode(lineTxt);
					StringBuilder content = new StringBuilder("");
					if(result[2] == null) {
						if(result[6] == null)
							content.append("<var namespace=\"\" expr=\"" + result[1] + "\" desc=\"\" lentype=\"VARLEN\" len=\""
									+ "\" loc=\"\" align=\"LEFT\" fill=\"#20\" compart=\"\" class=\"\" handleprocess=\"\" argvar=\"\" mac=\"\" />");
						else
							content.append("<var namespace=\"\" expr=\"" + result[1] + "\" desc=\"\" lentype=\"VARLEN\" len=\""
									+ result[6]
									+ "\" loc=\"\" align=\"LEFT\" fill=\"#20\" compart=\"\" class=\"\" handleprocess=\"\" argvar=\"\" mac=\"\" />");
						}
					else {
						if(result[6] == null)
							content.append("<var namespace=\"\" expr=\"" + result[1] + "\" desc=\"" + result[2] + "\" lentype=\"VARLEN\" len=\""
									+ "\" loc=\"\" align=\"LEFT\" fill=\"#20\" compart=\"\" class=\"\" handleprocess=\"\" argvar=\"\" mac=\"\" />");
						else
							content.append("<var namespace=\"\" expr=\"" + result[1] + "\" desc=\"" + result[2] + "\" lentype=\"VARLEN\" len=\""
									+ result[6]
									+ "\" loc=\"\" align=\"LEFT\" fill=\"#20\" compart=\"\" class=\"\" handleprocess=\"\" argvar=\"\" mac=\"\" />");
					}
					System.out.println(content);
				}
				read.close();
			} else {
				System.out.println("找不到指定的文件");
			}
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
	public static void main(String[] args) {
		readTxtFile("C:/Users/wasdw/Desktop/txt2Xml/23.txt");
	}
}
