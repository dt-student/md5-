# md5-
package com.demo.md5;

import java.io.*;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;


public class MdFive {

    public static void main(String[] args){

        String result = "";
        String encoding="UTF-8";

        File file = new File("C:\\Users\\Administrator\\Desktop\\md5.txt");

        if(file.isFile() && file.exists()) { //判断文件是否存在
            InputStreamReader read = null;//考虑到编码格式
            try {
                read = new InputStreamReader(new FileInputStream(file), encoding);
                BufferedReader bufferedReader = new BufferedReader(read);
                String lineTxt = null;
                while ((lineTxt = bufferedReader.readLine()) != null) {
                    MessageDigest md = MessageDigest.getInstance("MD5");
                    md.update(lineTxt.getBytes("UTF-8"));
                    byte b[] = md.digest();

                    int i;
                    StringBuffer buf = new StringBuffer("");

                    for(int offset=0; offset<b.length; offset++){
                        i = b[offset];
                        if(i<0){
                            i+=256;
                        }
                        if(i<16){
                            buf.append("0");
                        }
                        buf.append(Integer.toHexString(i));
                    }

                    result = buf.toString().toUpperCase();
                    System.out.println(result);
                }
            } catch (UnsupportedEncodingException e) {
                e.printStackTrace();
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (NoSuchAlgorithmException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
    }
}
