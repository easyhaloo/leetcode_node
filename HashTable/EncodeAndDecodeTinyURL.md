TinyURL is a URL shortening service where you enter a URL such as https://leetcode.com/problems/design-tinyurl and it returns a short URL such as http://tinyurl.com/4e9iAk.

Design the encode and decode methods for the TinyURL service. There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/encode-and-decode-tinyurl
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。







### 解析

>   题意大意是求URL的短地址，短地址与长地址之间相互映射。
>
> 可以使用Hash表来保存映射关系，然后使用随机数来组装短URL后缀



### 代码

```java
public class TinyURL {

  private static final Random RANDOM = new Random();

  private static final char[] chars = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'
      , 'a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l', 'z', 'x', 'c', 'v', 'b', 'n', 'm', 'Q', 'W', 'E', 'R', 'T', 'Y', 'Y', 'U', 'I', 'O', 'P',
      'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', 'Z', 'X', 'C', 'V', 'B', 'N', 'M'};


  private static final HashMap<String, String> MAP = new HashMap<>();

  private static final String TINY_URL_PREFIX = "http://tinyurl.com/";

  // Encodes a URL to a shortened URL.
  public String encode(String longUrl) {
    String shortUrl = MAP.get(longUrl);
    if (shortUrl == null) {
      shortUrl = TINY_URL_PREFIX + getRandomshort(6);
      MAP.put(longUrl, shortUrl);
      MAP.put(shortUrl, longUrl);
    }
    return shortUrl;
  }

  // Decodes a shortened URL to its original URL.
  public String decode(String shortUrl) {
    return MAP.getOrDefault(shortUrl, shortUrl);
  }

  private String getRandomshort(int len) {
    int i = 0;
    StringBuilder sb = new StringBuilder();
    while (i++ < len) {
      sb.append(chars[RANDOM.nextInt() % chars.length]);
    }
    return sb.toString();
  }

}

```

