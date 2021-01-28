package ytb;

import java.io.Serializable;

public class Phone implements Serializable{
	
	int phone;
	String name;
	String address;
	String email;
	String favorites ;
	
	public Phone() {
	}
	
	public Phone(int phone, String name, String address, String email, String favorites) {
		this.phone = phone;
		this.name = name;
		this.address = address;
		this.email = email;
		this.favorites = favorites;
	}
	
	public int getPhone() {
		return phone;
	}
	
	public void setPhone(int phone) {
		this.phone = phone;
	}
	
	public String getName() {
		return name;
	}
	
	public void setName(String name) {
		this.name = name;
	}
	
	public String getAddress() {
		return address;
	}
	
	public void setAddress(String address) {
		this.address = address;
	}
	
	public String getEmail() {
		return email;
	}
	
	public void setEmail(String email) {
		this.email = email;
	}
	
	public boolean setEmail1(String email1) {
		while (true) {
			// check xem email nhập đúng chưa
			if (email1 != null && email1.contains("@") && !email1.contains(" ")) {
				email = email1;
				return true;
			} else { 
				System.err.println("Email phải có @ và không có khoảng trắng !!!");
				return false;
			} 
		} 
	}
	
	public String getFavorites() {
		return favorites;
	}
	
	public void setFavorites(String favorites) {
		this.favorites = favorites;
	}
	
	public void show() {
			
		}
}
