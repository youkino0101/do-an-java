package ytb;

import java.util.Scanner;

public class Main {
	public static Scanner sc = new Scanner(System.in);
	
	// hàm main chính

	public static void main(String[] args) {
		String chooseMain = null;
		boolean exitMain = false;
		PhoneManager phoneManager = new PhoneManager();
		int phoneSdt;
		String phoneName;
		
		showMenu();
		while (true) {
			chooseMain = sc.next();
			switch (chooseMain) {
			case "1": 
				phoneManager.add();
				break;
			case "2":
				phoneSdt = phoneManager.inputPhone();
				phoneManager.editPhone(phoneSdt);
				break;
			case "3" :
				phoneName = phoneManager.inputName();
				phoneManager.editName(phoneName);
				break;
			case "4" :
				phoneManager.show();
				break;
			case "5" :
				phoneManager.sortPhoneByName();
				break;
			case "6" :
				phoneName = phoneManager.inputName();
				phoneManager.delete(phoneName);
				break;
			case "7" :
				phoneManager.deleteAll();
				break;
			case "8" :
				phoneName = phoneManager.inputName();
				phoneManager.searchName(phoneName);
				break;
			case "9" :
				phoneManager.favoritesList();
				break;
			case "0" :
				System.out.println("Bạn Đã Thoát Chương Trình\nGOODBYE");
				exitMain = true;
				break;
			default : 
				System.err.println("Chỉ Chọn Từ 0 - 8 !!!");
				break;
			}
			if (exitMain) {
				break;
			}
			showMenu();
		}
	}

	// các chức năng của chương trình
	
	private static void showMenu() {
		System.out.println("\n-------------------MENU DANH BẠ ---------------");
        System.out.println("1. THÊM DANH BẠ");
        System.out.println("2. CHỈNH SỬA DANH BẠ ĐÃ CÓ SẴN BẰNG SĐT");
        System.out.println("3. CHỈNH SỬA DANH BẠ ĐÃ CÓ SẴN BẰNG TÊN");
        System.out.println("4. HIỂN THỊ DANH BẠ");
        System.out.println("5. SẮP XẾP DANH BẠ THEO TÊN TỪ A-Z");
        System.out.println("6. XÓA 1 DANH BẠ THEO TÊN CÓ SẴN ");
        System.out.println("7. XÓA TOÀN BỘ DANH BẠ");
        System.out.println("8. TÌM KIẾM DANH BẠ THEO TÊN");
        System.out.println("9. HIỆN THỊ DANH MỤC YÊU THÍCH");
        System.out.println("0. THOÁT CHƯƠNG TRÌNH.");
        System.out.println("---------------------------");
        System.out.print("VUI LÒNG CHỌN: ");
	}
}
