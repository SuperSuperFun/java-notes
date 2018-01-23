```
package com.wangli.crawl;

import java.io.*;
import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLConnection;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Robot {
    public static void main(String[] args) {
        URL url = null;
        URLConnection urlConnection = null;
        BufferedReader br = null;
        PrintWriter pw = null;
        String reg = "http://[\\w+\\.?/?]+\\.[A-Za-z]+";
        //pattern是一个编译好的正则表达式
        Pattern pattern = Pattern.compile(reg);
        System.out.println(pattern);
        try {
            url = new URL("http://www.sina.com.cn");
            urlConnection = url.openConnection();
            br = new BufferedReader(new InputStreamReader(urlConnection.getInputStream()));
            pw = new PrintWriter(new FileWriter("C:\\Users\\super\\Desktop\\siteUrl.txt"), true);
            String buff = null;
            while ((buff=br.readLine()) != null) {
                /**
                 * Mather是一个正则表达式适配器，一般用pattern来获取一个Matcher对象
                 * 常用的方法有find()/group()
                 * boolean find()；
                 * find有点像一个迭代器，它能通过正则表达式向前迭代，当前方没有内容的时候，find会返回false
                 * */
                Matcher matcher = pattern.matcher(buff);
                while (matcher.find()) {
                    /**
                     * int groupCount() 返回所匹配的字符串的组数
                     * String group() 返回所匹配到的第0组的值，返回值String
                     * */
                    pw.println(matcher.group());
                }
            }
            System.out.println("爬取成功");
        } catch (MalformedURLException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                br.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            pw.close();
        }
    }
}

```
