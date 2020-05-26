# Test

import java.util.*;
import java.io.*;
import java.text.DecimalFormat;
import java.math.RoundingMode;
import java.io.FileNotFoundException;

import org.json.JSONException;
import org.json.JSONObject;

public class Main {

	public static void main(String[] args) throws IOException, JSONException {
		double[] a = new double[10000];
		JSONObject ob = new JSONObject();
		JSONObject ob1 = new JSONObject();
		File file = new File("F:\\Memory.txt");
		try (BufferedReader bf = new BufferedReader(new FileReader(file))) {
			String name1;
			int name=0,i=0;
			double total = 0.0,max = 0.0,temp;
			while ((name1 = bf.readLine()) != null) {
				if (name % 2 != 0) {
				    String s = name1;
					s = s.replaceAll("[^0-9]", "");
					s = s.trim();
					temp = Integer.parseInt(s);
					a[i++] = temp / 10000;
				}
				name++;
			}
			String s1;
			for (int j = 0; j < 938; j++) {
				s1 = String.format("%d", j);
				ob1.put(s1 + "s", a[j]);
				if (max < a[j])
					max = a[j];
				total = total + a[j];
			}
	        double average = total / 938;
			DecimalFormat df = new DecimalFormat("#.###");
			df.setRoundingMode(RoundingMode.CEILING);
			ob.put("AverageMemory(MB) ", df.format(average));
			ob.put("values: ", ob1);
			ob.put("MaximumMemory(MB)", df.format(max));
			System.out.println(ob);
		}
		
	}

}
