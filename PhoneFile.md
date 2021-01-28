package ytb;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.OutputStream;
import java.util.ArrayList;
import java.util.List;
 

public class PhoneFile {
    private static final String PHONE_FILE_NAME = "D:\\phone.txt";

    // ghi dữ liệu vào file 
    
    	public void write(List<Phone> phoneList) {
        FileOutputStream fos = null;
        ObjectOutputStream oos = null;
        try {
        	fos = new FileOutputStream(new File(PHONE_FILE_NAME));
            oos = new ObjectOutputStream(fos);
            oos.writeObject(phoneList);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            closeStream(fos);
            closeStream(oos);
        }
    }

    // đọc mảng từ file 

    public List<Phone> read() {
        List<Phone> phoneList = new ArrayList<>();
        FileInputStream fis = null;
        ObjectInputStream ois = null;
        try {
            fis = new FileInputStream(new File(PHONE_FILE_NAME));
            ois = new ObjectInputStream(fis);
            phoneList = (List<Phone>) ois.readObject();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            closeStream(fis);
            closeStream(ois);
        }
        return phoneList;
    }

    // đóng 
    
    private void closeStream(InputStream is) {
        if (is != null) {
            try {
                is.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    private void closeStream(OutputStream os) {
        if (os != null) {
            try {
                os.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    } 
}
