
- ### 代码

```java

package interview.array;
	
	import java.util.Arrays;
	
	/**
	 * 数组扩容工具
	 * 
	 * @author dell
	 *
	 */
	public class ArrayExpandUtils {
	
		private ArrayExpandUtils() {}
		/**
		 * 对数组扩容  给定指定的扩容长度
		 * @param sources 源数组
		 * @param newLen 扩容行政长度
		 * @return
		 */
		public static <T> T[] expandCapacity(T[] sources,int newLen) {
			newLen = newLen < 0 ? sources.length : sources.length+newLen;
			return Arrays.copyOf(sources, newLen);
		}
		
		/**
		 * 对数组进行默认1.5倍扩容
		 * @param sources 源数组
		 * @return
		 */
		public static <T> T[] expandCapacity(T[] sources) {
			int newLen = (sources.length*3)/2+1;
			return Arrays.copyOf(sources, newLen);
		}
		/**
		 * 对数组进行倍数扩容
		 * @param sources 源数据
		 * @param mulitiple 指定扩容倍数
		 * @return
		 */
		public static <T> T[] expandCapacityMul(T[] sources,int mulitiple) {
			mulitiple = mulitiple < 0 ? 1 : mulitiple;
			int newLen = sources.length*mulitiple;
			return Arrays.copyOf(sources, newLen);
		}
		
		public static void main(String[] args) {
		}
	}
	

```