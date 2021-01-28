package ytb;

import java.util.Collections;
import java.util.Comparator;
import java.util.List;
import java.util.Scanner;

public class PhoneManager extends Phone {
    public static Scanner sc = new Scanner(System.in);
    private List<Phone> phoneList;
    private PhoneFile phoneFile;
		
    public PhoneManager() {
    	phoneFile = new PhoneFile();
    	phoneList = phoneFile.read();
    }
    
 // thêm danh bạ
 
    public void add() {
    	int phone = inputPhone();
    	String name = inputName();
    	String address = inputAddress();
    	String email = inputEmail();
    	String phanloai = inputFavorites();
    	System.out.println("Bạn đã thêm danh bạ thành công!!!");
    	Phone ds = new Phone(phone, name, address, email, phanloai);
    	phoneList.add(ds);
    	phoneFile.write(phoneList);
    }
    
    // chỉnh sửa danh bạ bằng số điện thoại 
    
    public void editPhone(int phone) {
    	boolean kiemTra = false;
    	int size = phoneList.size();
    	for (int i = 0; i < size; i++) {
    		if (phoneList.get(i).getPhone() == phone) {
    			kiemTra = true;
    			phoneList.get(i).setName(inputName());
    			phoneList.get(i).setAddress(inputAddress());
    			phoneList.get(i).setEmail(inputEmail());
    			phoneList.get(i).setFavorites(inputFavorites());
    			System.out.println("Bạn đã cập nhật danh bạ thành công!!!");
    			break;
    		}
    	}
    	if (!kiemTra) {
    		System.out.printf("%d số này không có sẵn trong danh sách", phone);
    	} else {
    		phoneFile.write(phoneList);
    	}
    }
    
    // chỉnh sửa danh bạ bằng tên
    
    public void editName(String name) {
    	boolean kiemTraName = false;
    	int size = phoneList.size();
    	for (int i = 0; i < size; i++) {
    		if (phoneList.get(i).getName().equals(name)) {
    			kiemTraName = true;
    			phoneList.get(i).setPhone(inputPhone());
    			phoneList.get(i).setAddress(inputAddress());
    			phoneList.get(i).setEmail(inputEmail());
    			phoneList.get(i).setFavorites(inputFavorites());
    			System.out.println("Bạn đã cập nhật danh bạ thành công!!!");
    			break;
    		}
    	}
    	if (!kiemTraName) {
    		System.out.printf("%s tên này không có sẵn trong danh sách", name);
    	} else {
    		phoneFile.write(phoneList);
    	}
    }
          
    // xóa danh bạ theo tên có sẵn
    
    public void delete(String name) {
    	Phone ds = null;
    	int size = phoneList.size();
    	for (int i = 0; i < size; i++) {
            if (phoneList.get(i).getName().equalsIgnoreCase(name)) {
                ds = phoneList.get(i);
                break;
            }
        }
        if (ds != null) {
            phoneList.remove(ds);
            phoneFile.write(phoneList);
            System.out.println("Bạn đã xóa thành công");
        } else {
        	System.out.printf("Không tìm thấy danh bạ cần xóa");
        }
    }
    
    // xóa toàn bộ danh bạ hiện có
    
    public boolean deleteAll() {
    	System.out.println("Bạn có chắc là muốn xóa toàn bộ danh bạ không?");
    	System.out.println("Có: 1                Không: 0");
    	System.out.println("Vui lòng chọn 1 hoặc 0: ");
    	while (true) {
    		String chose = sc.next();
    		switch (chose) {
    		case "1":
    			phoneList.clear();
    	    	phoneFile.write(phoneList);
    	    	System.out.println("Bạn đã xóa thành công");
    	    	return true;
    		case "0": 
    			return true;
    		default: 
    			System.out.println("Chỉ chọn 0 (không) và 1 (có)");
    			System.out.println("Vui lòng nhập lại:");
    			break;
    		}
    	}
    }
    
    // hiện thị danh bạ
    
    public void show() {
    	System.out.println("----------------------------------------Danh Sách Danh Bạ Của Bạn----------------------------------");
    	System.out.println("___________________________________________________________________________________________________");
    	System.out.printf("\n|%20s|%13s|%25s|%30s|%10s|", "Tên", "Số Điện Thoại", "Địa chỉ", "Email", "Yêu Thích");
    	for (Phone db : phoneList) {
    		System.out.printf("\n|%20s|   %010d|%25s|%30s|%10s|\n", db.getName(), db.getPhone(), db.getAddress(),
    															db.getEmail(), db.getFavorites());
    	}
    	System.out.println("___________________________________________________________________________________________________");

    }
    
    // sắp xếp danh bạ
    
    public void sortPhoneByName() {
        Collections.sort(phoneList, new Comparator<Phone>() {
        	public int compare(Phone a1, Phone a2) {
        		return a1.getName().compareTo(a2.getName());
        	}
        });
        phoneFile.write(phoneList);
        show();
    }
    
    // tìm kiếm danh bạ theo tên
    
    public void searchName(String name) {
    	Phone ds = null;
    	boolean checkSearch = false;
    	int size = phoneList.size();
    	for (int i = 0; i < size; i++) {
    		if (phoneList.get(i).getName().equalsIgnoreCase(name)) {
    			checkSearch = true;
    			ds = phoneList.get(i);
    			break;
    		}
    	}
    	if (checkSearch) {
    		System.out.println("Đã tìm thấy tên cần tìm !!!");
    		System.out.printf("\n|%20s|%13s|%25s|%30s|%10s|", "Tên", "Số ĐT", "Địa chỉ", "Email", "Yêu Thích");
    		System.out.printf("\n|%20s|   %010d|%25s|%30s|%10s|\n", ds.getName(), ds.getPhone(), ds.getAddress(),
																ds.getEmail(), ds.getFavorites());
    	} else {
    		System.err.println("Không tìm thấy tên cần tìm!!!");
    	}
    }
    
    // hiển thị danh sách yêu thích
    
    public void favoritesList() {
    	Phone ds = null;
    	int size = phoneList.size();
    	System.out.printf("\n|%20s|%13s|%25s|%30s|%10s|", "Tên", "Số ĐT", "Địa chỉ", "Email", "Yêu Thích");
    	for (int i = 0; i < size; i++) {
    		boolean checkFavorites = false;
    		for (int j = 0; j <= i; j++) {
    			if (phoneList.get(i).getFavorites().equals("x")) {
    			ds = phoneList.get(i);
    			checkFavorites = true;
    			break;
    			}
    		}
	    	if (checkFavorites) {
	    		System.out.printf("\n|%20s|   %010d|%25s|%30s|%10s|\n", ds.getName(), ds.getPhone(), ds.getAddress(),
																	ds.getEmail(), ds.getFavorites());
	    	}
    	}
    }
    
   // nhập tên
    
    public String inputName() {
        System.out.println("Nhập vào tên: ");
    	return sc.nextLine();
    }
    
    // nhập số điện thoại
     
    public int inputPhone() {
    	System.out.println("Nhập vào số điện thoại: ");
    	while (true) {
    		try {
    			int phone1 = Integer.parseInt((sc.nextLine()));
      			return phone1;
    		} catch (NumberFormatException ex) {
    			System.err.println("Lưu ý chỉ nhập kí tự số !!!");		
    		}
    	}
    }
    
    // nhập địa chỉ
    
    public String inputAddress() {
        System.out.println("Nhập vào địa chỉ: ");
        return sc.nextLine();
    }
    
    // nhập email
    
    public String inputEmail() {
    	inputEmail1();
    	return email;
    }
    
    //  lựa chọn về việc cần thêm email hay không
    
    public boolean inputEmail1() {
    	System.out.println("Bạn có muốn thêm email cho số này không?");
    	System.out.println("Có: 1                Không: 0");
    	System.out.println("Vui lòng chọn 1 hoặc 0: ");
    	while (true) {
    		String chose = sc.next();
    		switch (chose) {
    		case "1":
    			checkEmail();
    			return true;
    		case "0": 
    			email = "";
    			return true;
    		default: 
    			System.out.println("Chỉ chọn 0 (không) và 1 (có)");
    			System.out.println("Vui lòng nhập lại:");
    			break;
    		}
    	}
    }
    
    // kiểm tra xem email có nhập đúng hay không
    
    public void checkEmail() {
    	while (true) {
    		System.out.println("Nhập vào email của bạn: ");
    		String checkEmail = sc.next();
    		boolean check = setEmail1(checkEmail);
    		if (check) {
    			break;
    		}
    	}
    }
    
    // nhập mục yêu thích
       
    public String inputFavorites() {
    	inputFavorites1();
    	return favorites;
    }
    
    // lựa chọn có thêm vào mục yêu thích hay không
    
    public boolean inputFavorites1() {
        System.out.println("Bạn có muốn thêm vào mục yêu thích không? ");
        System.out.println("Có: 1                Không: 0");
    	System.out.println("Vui lòng chọn 1 hoặc 0: ");
    	while (true) {
    		String chosePhanLoai = sc.next();
    		switch (chosePhanLoai) {
    		case "1":
    			System.out.println("Bạn đã thêm vào mục yêu thích");
    			favorites = "x";
    			return true;
    		case "0": 
    			favorites = "";
    			return true;
    		default: 
    			System.out.println("Chỉ chọn 0 (không) và 1 (có)");
    			System.out.println("Vui lòng nhập lại:");
    			break;
    		}  
    	}
    }
    
    // getter và setter cho phần mảng
    
    public List<Phone> getPhoneList() {
    	return phoneList;
    }
    
    public void setPhoneList(List<Phone> phoneList) {
    	this.phoneList = phoneList;
    }
}

