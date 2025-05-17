
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Scanner;
import java.time.DayOfWeek;
import java.time.LocalDate;
import java.time.YearMonth;
import java.time.format.DateTimeFormatter;
import java.time.temporal.ChronoUnit;

public class FinalProject {
	
	static Scanner scan = new Scanner (System.in);
	static int quantity = 0;
	static 	int BookId = 1;
	static String Account;
	static int limit = 0;
    static int returncode = 1;

	public static void main(String[] args) throws IOException {
		startingmenu();
	}
	
	private static void startingmenu() throws IOException {
		boolean flag = true;
		while(flag) {
			System.out.println("╔═══════════════════════════════════════════════╗");
			System.out.println("║    (^_^)    Welcome to Galvez Library~!       ║");
			System.out.println("║       *~ Where books come to life! ~*         ║");
			System.out.println("╠═══════════════════════════════════════════════╣");
			System.out.println("║                                               ║");
			System.out.println("║   [1] Login as Admin / Librarian              ║");
			System.out.println("║   [2] Create an Admin/Librarian Account       ║");
			System.out.println("║   [3] Exit the Library                        ║");
			System.out.println("║                                               ║");
			System.out.println("╚═══════════════════════════════════════════════╝");
			System.out.print("Please choose an option [1-3]: ");
			int choice = scan.nextInt();
			
			switch(choice) {
			case 1: 
				
			    BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\AccountsLibrary.txt"));
				if(reader.readLine() == null) {
					System.out.println("THERES NO ACCOUNT YET. CREATE A NEW ONE");
	                logTransaction("Tried to Log in But there is no Account yet");

					break;
				}		
				
				reader.close();
				
			    BufferedReader Inputreader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\AccountsLibrary.txt"));
			    System.out.println("ENTER YOUR USERNAME");
			    String username = scan.next();			    
			 
			    boolean found = false;
			    
			    String line;
			    while ((line = Inputreader.readLine()) != null) {
			    String[] arr = line.split("\\*");
		        if (username.equals(arr[0]) && arr[1].equalsIgnoreCase("admin")) {
	            Account = username;
	            spacer();
	            System.out.println("Successfully Logged In | Welcome Admin");
	            found = true;
                logTransaction("Admin Successfully Log in: " + username);
	            Inputreader.close();
	            adminmenu();
	            break;
		        } 
		        else if (username.equals(arr[0]) && arr[1].equalsIgnoreCase("librarian")) {
		        Account = username;
		        System.out.println("Successfully Logged In | Welcome Librarian");
		        found = true;
                logTransaction("Librarian Successfully Log in: " + username);
	            Inputreader.close();
	            librarianmenu();
	            break;
				        }
				    }

				    if (!found) {
				        System.out.println("INVALID USERNAME! TRY AGAIN.");
				    }
				    
				    break;

			case 2:
				int flag1 = 0;
				System.out.println("\n+----------------------------------------------+");
		        System.out.println("|               Account Creation               |");
		        System.out.println("+----------------------------------------------+");
		        System.out.println("|     What Account would you like to create    |");
		        System.out.println("| [1] Admin Account                            |");
		        System.out.println("| [2] Librarian Account                        |");
		        System.out.println("| [0] Back to Admin Menu                       |");
		        System.out.println("+----------------------------------------------+");
				int input = scan.nextInt();
				
				if(input == 0) {
					startingmenu();
				}else {
				
				System.out.println("| What Username would you like?  |              |");
				String newAccount = scan.next();

				String account = null;
				if(input == 1) {
					account = "ADMIN";
					flag1 = 1;
				}else if(input == 2) {
					account = "LIBRARIAN";
					flag1 = 1;
				}else {
					System.out.println("INVALID CHOICE");
				}
				
			
				if(flag1 == 1) {
				BufferedWriter writer = new BufferedWriter(new FileWriter("C:\\Users\\Kobe\\Downloads\\AccountsLibrary.txt", true));
				writer.write(newAccount + "*" + account +"*" + "\n");
				writer.close();
				System.out.println(newAccount + " YOUR |" +  account+  "| ACCOUNT HAS BEEN CREATED");	
                logTransaction("New " + account + " Account Created: " + newAccount);
				spacer();
				}
			}	
			case 3:
				System.out.println("THANK YOU ");
				flag = false;
				break;
			default:
				System.out.println("Invalid Number ");
				System.out.println("Would you like to try again? [Y/N]  ");
				String continues = scan.next();
				
				if(continues.equalsIgnoreCase("N")) {
					System.out.println("THANK YOU ");
					flag = false;
				}
		}

		}
	}
	private static void adminmenu() throws IOException {

		System.out.println("======================================");
		System.out.println("Account name:" + Account +"\t" + "VIEWING: ADMIN |");
		System.out.println("======================================");

		boolean flag = true;
		
		while (flag) {
			    System.out.println("\n+------------------------------------------------------+");
		        System.out.println("|📖 Welcome Admin to the Library Management System       |");
		        System.out.println("+--------------------------------------------------------+");
		        System.out.println("| [1] Add Student Details                                |");
		        System.out.println("| [2] Update Student Detail                              |");
		        System.out.println("| [3] Add Book						                     |");
		        System.out.println("| [4] View Reports                                       |");
		        System.out.println("| [5] Archive/Unarchive Book                             |");
		        System.out.println("| [6] Back to Main Menu                                  |");
		        System.out.println("| [0] EXIT                                               |");
		        System.out.println("+--------------------------------------------------------+");

		        System.out.print("Choose an option: \n");
				int choice1 = scan.nextInt();
				
				spacer();
				
				switch(choice1) {
				case 1: addStudent();
						break;
				case 2: updateStudent();
						break;
				case 3: addBook();
						break;
				case 4:   
				System.out.println("\n+------------------------------------------------------+");
		        System.out.println("|📖 	Welcome to View Reports                              |");
		        System.out.println("+--------------------------------------------------------+");
		        System.out.println("| [1] View Books                                         |");
		        System.out.println("| [2] View All Student Details                           |");
		        System.out.println("| [3] View All Transaction Logs                          |");
		        System.out.println("| [0] Back to Admin Menu                                 |");
		        System.out.println("+--------------------------------------------------------+");
		        int chosen = scan.nextInt();
		        
		        spacer();
		        if(chosen == 1) {
					viewBook();//student and all logs and all books so need ko ilagay both here
		        }else if(chosen == 2) {
		        	System.out.println("+----------All Students Info----------+");
		        	viewStudent();
		        }else if(chosen == 3) {
		        	viewTransactions();
		        }
						break;
				case 5: archiveBook();
						break;
				case 6: startingmenu();
						break;
				case 0:	System.out.println("GOODBYE THANKS FOR VISITING");
						flag = false;
						break;
				default: 
					System.out.println("INVALID CHOICE TRY AGAIN");
				}
		}

	}
	
	private static void librarianmenu() throws IOException {
		boolean flag = true;
		
		while(flag) {
		  System.out.println("\n+------------------------------------------------------+");
	      System.out.println("|📖 Welcome Librarian to the Library Management System   |");
	      System.out.println("+--------------------------------------------------------+");
          System.out.println("| [1] Transact/Borrow books                              |");
          System.out.println("| [2] Transact/Return books                              |");
          System.out.println("| [3] Back to Main Menu                                  |");
          System.out.println("| [0] EXIT                                               |");
	      System.out.println("+--------------------------------------------------------+");
		        
	      System.out.print("Choose an option: \n");
	      int choice1 = scan.nextInt();
			
			switch(choice1) {
			case 1: borrowBook();
					break;
			case 2: returnbook();
					break;
			case 3: startingmenu();
					break;
			case 0: System.out.println("GOODBYE THANKS FOR VISITNG");
					flag = false;
					break;
			}
		}
		
	}
	private static void addStudent() throws IOException {
		int create = 0;
		BufferedWriter writer = new BufferedWriter(new FileWriter("C:\\Users\\Kobe\\Downloads\\USERDETAILSHCI.txt", true));
		System.out.println("ENTER THE STUDENT NAME: ");
		String Studentname = scan.next();
		
		System.out.println("ENTER THE STUDENTS ID#");
		String StudentID = scan.next();
		
		
		System.out.println("ENTER THE STUDENT COURSE: ");
		String course = scan.next();
		
		String standing = "Enable"; //enabled || Disabled
		System.out.println("SUCCESSFULLY ADDED! ");
				
	BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\USERDETAILSHCI.txt"));		
		String line;
		while((line = reader.readLine()) != null) {
			String[] arr = line.split("\\*");
			if(Studentname.equalsIgnoreCase(arr[0]) && StudentID.equals(arr[1]) && arr[2].equalsIgnoreCase(course)) {
				System.out.println("STUDENT ACCOUNT ALREADY CREATED| /n"
						+ "CREATE A NEW ONE");
				create =1;
			}
		}
		reader.close();
		if(create == 0) {
			String combined = Studentname + "*" + StudentID + "*" + course + "*" + standing + "*" + "\n";
			writer.write(combined);
			writer.close();
		}
	}
	
	private static void updateStudent() throws IOException {
		File tempfile = new File("C:\\Users\\Kobe\\Downloads\\studentdetailstemp.txt");
		File studentRecords = new File("C:\\\\Users\\\\Kobe\\\\Downloads\\\\USERDETAILSHCI.txt");
		
	    System.out.println("\n+----------------------------------------------+");
        System.out.println("|            STUDENT STATUS MENU               |");
        System.out.println("+----------------------------------------------+");
        System.out.println("| [1] Disable Student                          |");
        System.out.println("| [2] Enable Student                           |");
        System.out.println("| [3] Update All Info                          |");
        System.out.println("| [0] Back to Admin Menu                       |");
        System.out.println("+----------------------------------------------+");
        System.out.println("Enter the Number to set student status: ");
        String choice = scan.next();
        
      	viewStudent();
		System.out.println();
		
        switch (choice) {
        case "1":
           	System.out.print("Enter ID of Student to Update: ");
    	    String code = scan.next();
    	    boolean hanap = false;
    	    BufferedReader reader = new BufferedReader(new FileReader(studentRecords));
    	    BufferedWriter writer = new BufferedWriter(new FileWriter(tempfile));

    	    String parts;
    	    while ((parts = reader.readLine()) != null) {
    	        String[] fields = parts.split("\\*");
    	        if (fields.length == 4 && fields[1].equals(code)) {
    	            if (fields[3].trim().equalsIgnoreCase("ENABLE")) {//lalagyan sa createRecords
    	            	hanap = true;
    	                fields[3] = "DISABLE";
    	                System.out.println("Student with ID " + code + " Account Disabled successfully!");
    	                logTransaction("Student with ID " + code + " Account Disabled");
    	            }
    	            writer.write(String.join("*", fields) + "\n");
    	        } else {
    	            writer.write(parts + "\n");
    	        }
    	    }
    	    reader.close();
    	    writer.close();
    	    reader = new BufferedReader(new FileReader(tempfile));
    	    writer = new BufferedWriter(new FileWriter(studentRecords));

    	    String track;
    	    while ((track = reader.readLine()) != null) {
    	        writer.write(track + "\n");
    	    }
    	    reader.close();
    	    writer.close();
    	    tempfile.delete();
    	    break;
    	    
        case "2": 
        	System.out.print("Enter ID of Student to Update: ");
    	    String code1 = scan.next();
    	    boolean hanap1 = false;

    	    BufferedReader reader1 = new BufferedReader(new FileReader(studentRecords));
    	    BufferedWriter writer1 = new BufferedWriter(new FileWriter(tempfile));

    	    String parts1;
    	    while ((parts1 = reader1.readLine()) != null) {
    	        String[] fields = parts1.split("\\*");
    	        if (fields.length == 4 && fields[1].equals(code1)) {
    	            if (fields[3].trim().equalsIgnoreCase("DISABLE")) {//lalagyan sa createRecords
    	            	hanap1 = true;
    	                fields[3] = "ENABLE";
    	                System.out.println("Student with ID " + code1 + " Account Enabled successfully!");
    	                logTransaction("Student with ID " + code1+ " Account Enabled");
    	            }
    	            writer1.write(String.join("*", fields) + "\n");
    	        } else {
    	        	writer1.write(parts1 + "\n");
    	        }
    	    }
    	    reader1.close();
    	    writer1.close();
    	    
    	    reader1 = new BufferedReader(new FileReader(tempfile));
    	    writer1 = new BufferedWriter(new FileWriter(studentRecords));

    	    String track1;
    	    while ((track1 = reader1.readLine()) != null) {
    	    	writer1.write(track1 + "\n");
    	    }
    	    reader1.close();
    	    writer1.close();
    	    tempfile.delete();
    	    break;

        case "3":
    		
    		BufferedReader Filereader = new BufferedReader(new FileReader(studentRecords));
    		BufferedWriter Tempwriter = new BufferedWriter(new FileWriter(tempfile));
    		
    		String link;
    		while((link = Filereader.readLine()) != null) {
    			Tempwriter.write(link +"\n");			//NALIPAT NA SA TEMP
    		}
    		
    		Filereader.close();
    		Tempwriter.close();
    		
    		BufferedReader Tempreader = new BufferedReader(new FileReader(tempfile));
    		BufferedWriter Filewriter = new BufferedWriter(new FileWriter(studentRecords));
    		int found = 0;
    		System.out.println("ENTER STUDENT ID TO UPDATE INFO: ");
    		String IDtoupdate = scan.next();
    		
    		String line;
    		while((line = Tempreader.readLine()) != null) {
    			String[] field = line.split("\\*");
    			if(field.length == 4 && field[1].equals(IDtoupdate)) {
    				System.out.println("ENTER NEW NAME");
    				String newname = scan.next();
    				System.out.println("ENTER NEW STUDENT ID");
    				String newID = scan.next();
    				System.out.println("ENTER NEW COURSE:");
    				String newcourse = scan.next();
    				System.out.println("SUCCESSFULLY UPDATED! ");
    				line = newname + "*" + newID + "*" + newcourse + "*" + field[2] + "*" + "\n";
    				found = 1;
    			}
    			Filewriter.write(line);
    		}
    		
    		if(found == 0) {
    			System.out.println("STUDENT ID NOT FOUND PLEASE TRY AGAIN! ");
    		}
    		Tempreader.close();
    		Filewriter.close();
    		tempfile.delete();
        	break;
        }
	}
	private static void viewStudent() throws IOException {
		BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\USERDETAILSHCI.txt"));
		
		String line;
		System.out.println("Name | \t" + " StudentID |");
		while((line = reader.readLine()) != null) {
			String[] arr = line.split("\\*");
			System.out.println(arr[0] + "\t|\t" + arr[1] + "\t|\t" + arr[2] + "\t|\t" + arr[3]);
		}
			
	}
	
	private static void addBook() throws IOException {
	 BufferedWriter geekwrite = new BufferedWriter(new FileWriter("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt", true));
	 	System.out.println("WHAT GENRE IS YOUR BOOK | [1] MATH | [2] SCIENCE | [3] IT? ");
		int code = scan.nextInt();
		
		if(code == 1 || code == 2 || code == 3) {
			String genre = "";
			if(code == 1) {
				genre  = "MATH";
			}else if(code == 2) {
				genre = "SCIENCE";
			}else if(code == 3) {
				genre = "IT";
			}

			System.out.println("ENTER BOOK TITLE: ");
			String Title = scan.next();
			
			System.out.println("ENTER THE AUTHOR: ");
			String Author = scan.next();
			
			String status = "Available";
			
			System.out.println("BOOK SUCCESSFULLY ADDED!: ");
			String combine = BookId + "*" + genre + "*" + Title + "*" + Author + "*" + status + "*";
			geekwrite.write(combine + "\n");
			quantity++;
			BookId++;
			geekwrite.close();
		}else {
			System.out.println("INVALID GENRE");
		}
	}
	
	private static void viewAllBook() throws IOException {
		BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt"));
		
		   String line;
		    System.out.println("BookId |" + " Genre  |" + " Title |" + " Author |" + " Status");
		    while ((line = reader.readLine()) != null) {
		        String[] arr = line.split("\\*");
		        if (arr.length >= 5) {
		            System.out.println(arr[0] + " \t" + arr[1] + " \t " + arr[2] + " \t" + arr[3] + "\t" + arr[4]);
		        }
	}
		    reader.close();
}

	
	private static void viewBook() throws IOException {
		
		BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt"));
		System.out.println("[1] view all or [2] by genre??? [3] Exit ");
		int choice = scan.nextInt();
		
		if(choice == 2) {
			int counter = 1;
			System.out.println("what genre to look for | [1] MATH | [2] SCIENCE | [3] IT?");
			int genretolookcode = scan.nextInt();
			
			String genretolook = "";
			if(genretolookcode == 1) {
				genretolook = "MATH";
			}else if(genretolookcode == 2) {
				genretolook = "SCIENCE";
			}else if(genretolookcode == 3) {
				genretolook = "IT";
			}else {
				System.out.println("INVALID CODE! ");
			}
			
			
			String line;
			System.out.println("BookId |" + " Genre |"  + "  Title |" + " Author |" + " Status");
			while((line = reader.readLine()) != null) {
				String[] arr = line.split("\\*");
				if(genretolook.equalsIgnoreCase(arr[1])) {				
				System.out.println(arr[0] + " \t" + arr[1] + " \t" + arr[2] + " \t" + arr[3] + "\t" + arr[4]);
				}
		
			counter++;
		}
	}
		
			// READ MUNA NASA INPUT FILE
		
		if (choice == 1) { // View all books
			viewAllBook();
    }
		
		if(choice == 3) {
			System.out.println();
			adminmenu();
		}
	}	
	private static void archiveBook() throws IOException {
		
		System.out.println("[1]: Archive");
		System.out.println("[2]: Unarchive");
		System.out.println("[3]: Exit/Back");
		int choice = scan.nextInt();
			
		if(choice == 1) {
			File tempfile = new File("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt.temp");
		    BufferedReader fileReader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt"));
		    BufferedWriter tempWriter = new BufferedWriter(new FileWriter(tempfile));

		    String line;
		    while ((line = fileReader.readLine()) != null) {
		        tempWriter.write(line + "\n");
		    }

		    fileReader.close();
		    tempWriter.close();
		    
			BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt"));
			
			   String link;
			   System.out.println("BookId |" + " Genre  |" + " Title |" + " Author |" + " Status");		
			   while ((link = reader.readLine()) != null) {
			   String[] arr = link.split("\\*");
			   	if (arr.length >= 5 && !arr[4].equals("ARCHIVED")) {
				   System.out.println(arr[0] + " \t" + arr[1] + " \t " + arr[2] + " \t" + arr[3] + "\t" + arr[4]);
				   		}    
			   	}

		    BufferedReader tempReader = new BufferedReader(new FileReader(tempfile));
		    BufferedWriter fileWriter = new BufferedWriter(new FileWriter("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt"));
		    
		    System.out.println("ENTER BOOK ID TO ARCHIVE:");
		    String bookArchive = scan.next();
		    boolean found = false;

		    while ((line = tempReader.readLine()) != null) {
		        String[] arr = line.split("\\*");
		        if (arr.length >= 5 && arr[0].equals(bookArchive)) {
		            if (arr[4].equalsIgnoreCase("ARCHIVED")) {
		                System.out.println("Book is already archived!");
		            } else if(arr[4].equalsIgnoreCase("OUT")) {
		            	System.out.println("Cannot Archive this book currently |Outside| ");
		            }
		            else {
		                arr[4] = "ARCHIVED";
		                System.out.println("Book Found To Be Available");
		                System.out.println("SUCCESSFULLY ARCHIVED!");
		            }
		            found = true;
		        }

		        String updatedLine = arr[0] + "*" + arr[1] + "*" + arr[2] + "*" + arr[3] + "*" + arr[4] + "*";
		        fileWriter.write(updatedLine + "\n");
		    }

		    if (!found) {
		        System.out.println("INVALID BOOK ID! TRY AGAIN");
		    }

		    tempReader.close();
		    fileWriter.close();
		    tempfile.delete();
		}
		else if(choice == 2) {
			File tempfile = new File("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt.temp");
		    BufferedReader fileReader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt"));
		    BufferedWriter tempWriter = new BufferedWriter(new FileWriter(tempfile));

		    String line;
		    while ((line = fileReader.readLine()) != null) {
		        tempWriter.write(line + "\n");
		    }

		    fileReader.close();
		    tempWriter.close();
		    
			BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt"));
			
			   String link;
			   System.out.println("BookId |" + " Genre  |" + " Title |" + " Author |" + " Status");		
			   while ((link = reader.readLine()) != null) {
			   String[] arr = link.split("\\*");
			   	if (arr.length >= 5 && arr[4].equals("ARCHIVED")) {
				   System.out.println(arr[0] + " \t" + arr[1] + " \t " + arr[2] + " \t" + arr[3] + "\t" + arr[4]);
				   		}    
			   	}
				   
			    BufferedReader tempReader = new BufferedReader(new FileReader(tempfile));
			    BufferedWriter fileWriter = new BufferedWriter(new FileWriter("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt"));
			    
			    System.out.println("ENTER BOOK ID TO UNARCHIVE:");
			    String bookArchive = scan.next();
			    boolean found = false;

			    while ((line = tempReader.readLine()) != null) {
			        String[] arr = line.split("\\*");
			        if (arr.length >= 5 && arr[0].equals(bookArchive)) {
			            if (arr[4].equalsIgnoreCase("ARCHIVED")) {
			                System.out.println("Book Found To Be ARCHIVED");
			                System.out.println("SUCESSFULLY UNARCHIVED! ");
			                arr[4] = "Available";
			            }
			            else {
			            	System.out.println("INVALID BOOK ID TRY AGAIN:");
			            }
			        }

			        String updatedLine = arr[0] + "*" + arr[1] + "*" + arr[2] + "*" + arr[3] + "*" + arr[4] + "*";
			        fileWriter.write(updatedLine + "\n");
			    }

			    tempReader.close();
			    fileWriter.close();
			    tempfile.delete();
		}else if(choice == 3) {
			spacer();
			adminmenu();
		}else {
			System.out.println("INVALID CHOICE [ 1-3 Only ]");
			System.out.println("Returning to Main Menu");
			spacer();
		}
	
	}
			
	private static void borrowBook() throws IOException {
	    int flag = 0;
	    boolean validStudent = false;
	    boolean shouldDisable = false;
	    
	    System.out.println("ENTER YOUR STUDENT NAME ");
	    String name = scan.next();

	    System.out.println("ENTER YOUR STUDENT ID");
	    String StudentID = scan.next();
	    String info;

	    BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\USERDETAILSHCI.txt"));
	    ArrayList<String> userLines = new ArrayList<>();
	    while ((info = reader.readLine()) != null) {
	        String[] arr = info.split("\\*");
		    //checker if all condition for student is met
	        if (arr.length >= 3 && arr[0].equalsIgnoreCase(name) && arr[1].equals(StudentID) && arr[3].equalsIgnoreCase("Enable")) {
	            
	            validStudent = true;
	            if (limit == 2) {
	                arr[3] = "DISABLE"; // Mark for update
	                shouldDisable = true;
	               info = arr[0] + "*" + arr[1] + "*" + arr[2] + "*" + arr[3];
	            }
	        }
			userLines.add(info); // Keep original or modified line
	    }
	    
	    if (validStudent && shouldDisable) {
	        try (BufferedWriter writer = new BufferedWriter(
	            new FileWriter("C:\\Users\\Kobe\\Downloads\\USERDETAILSHCI.txt"))) {
	            
	            for (String updatedLine : userLines) {
	                writer.write(updatedLine);
	                writer.newLine();
	            }
	        }
	        System.out.println("Student account disabled (reached 2-book limit)");
	    }
	    
	    reader.close();

	    // Count how many books the student already borrowed
	    BufferedReader borrowCountReader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\UNAVAILABLEBOOKSOROUTSIDE.txt"));
	    String borrowedLine;
	    while ((borrowedLine = borrowCountReader.readLine()) != null) {
	        String[] parts = borrowedLine.split("\\*");
	        //CHECKER IF NAREACH NA LIMIT
	        if (parts.length >= 4 && parts[0].equalsIgnoreCase(name) && parts[1].equals(StudentID) && Integer.parseInt(parts[3]) >= 2 && parts[4].equalsIgnoreCase("OUT")) {
	        	   System.out.println("YOU HAVE REACHED THE BORROW LIMIT (2 BOOKS). RETURN FIRST TO BORROW AGAIN.");
		            return;
		            //need to disable na sa student details para di na makahiram
	        }
	    }
	    borrowCountReader.close();
	            
	    if (validStudent && !shouldDisable) {
	    	
	    	File originalFile = new File("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt");
	        File tempFile = new File("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt.temp");

	        BufferedReader Filereader = new BufferedReader(new FileReader(originalFile));
	        boolean anyAvailableBooks = false;
	        String line;
	        while ((line = Filereader.readLine()) != null) {
	            String[] arr = line.split("\\*");
	            //CHECK IF THERES ANY BOOKS
	            if (arr.length >= 5 && !arr[4].equalsIgnoreCase("ARCHIVED") && !arr[4].equalsIgnoreCase("OUT")) {
	                anyAvailableBooks = true;
	                break;
	            }
	        }

	        Filereader.close();
	        
	        BufferedWriter Tempwriter = new BufferedWriter(new FileWriter("C:\\Users\\Kobe\\Downloads\\UNAVAILABLEBOOKSOROUTSIDE.txt", true));
	        //IF WALA
	        if (!anyAvailableBooks) {
	            System.out.println("\n*** NO AVAILABLE BOOKS - ALL BOOKS ARE ARCHIVED OR BORROWED ***\n");
	            Filereader.close();
	            Tempwriter.close();
	            return;
	        }
	        //IF MERON
	        Filereader = new BufferedReader(new FileReader(originalFile));
	        
	        System.out.println("\n+----------------------------------------------+");
	        System.out.println("|         All the available books are \n         |");
	        System.out.println("+------------------------------------------------+");
	        System.out.println("+---BookId | Genre | Title | Author | Status |---+"); 
	        while ((line = Filereader.readLine()) != null) {
	            String[] arr = line.split("\\*");
	            if (arr.length >= 5 && !arr[4].equals("ARCHIVED") && !arr[4].equalsIgnoreCase("out")) {
	                System.out.println("\t" + arr[0] + " \t" + arr[1] + " \t" + arr[2] + " \t" + arr[3] + " \t" + arr[4]);
	            }
	        }
	      	 System.out.println("+------------------------------------------------+");
	        Filereader.close();
	        
	        //lipat to temp
	        BufferedReader Filereaderdin = new BufferedReader(new FileReader(originalFile));
	        BufferedWriter TempWriter = new BufferedWriter(new FileWriter(tempFile));
	        
	        while ((line = Filereaderdin.readLine()) != null) {
	            TempWriter.write(line +"\n");
	        }
	        
	        Filereaderdin.close();
	        TempWriter.close();
	        
	        //nalipat na sa temp
	        
	        System.out.println("Which one would you like to borrow? Enter its BookId:");
	        String Booktoborrow = scan.next();
	        
	        BufferedReader Tempreaders = new BufferedReader(new FileReader(tempFile));
	        BufferedWriter OriginalWriter = new BufferedWriter(new FileWriter(originalFile));
	        
	        boolean found = false;
	        String link;
	        while ((link = Tempreaders.readLine()) != null) {
	            String[] ass = link.split("\\*");

	            if (ass.length >= 5) {
	                if (ass[0].equalsIgnoreCase(Booktoborrow)) {
	                    if (ass[4].equalsIgnoreCase("OUT")) {
	                        System.out.println("BOOK IS ALREADY BORROWED/OUTSIDE");
	                    } else if (ass[4].equalsIgnoreCase("ARCHIVED")) {
	                        System.out.println("CANNOT BORROW THIS BOOK: ARCHIVED");
	                    } else {
	                    	
	                    	System.out.println("Book found. Do you wish to proceed? [Y] [N] ");
		                	String choice1 = scan.next();
		                	if(choice1.equalsIgnoreCase("Y")) {
		                	     ass[4] = "OUT";
			                        found = true;
			                        System.out.println("SUCCESSFULLY BORROWED!");
			                        limit++;
			                        
			                        //dates
			                        BufferedWriter BorrowWriter = new BufferedWriter(new FileWriter("C:\\Users\\Kobe\\Downloads\\Borrow&Due.txt", true));
			                        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
			                        // Get current date and due date
			                        
			                        LocalDate borrowDate = LocalDate.now();
			                        LocalDate dueDate = null;
			                        if(limit == 1) {
				                        LocalDate dueDatetemp = borrowDate.plusDays(1);
				                        dueDate = dueDatetemp;
			                        }else if(limit == 2) {
				                        LocalDate dueDatetemp = borrowDate.plusDays(2);
				                        dueDate = dueDatetemp;
			                        }
			                        LocalDate today = LocalDate.now();
			                        
			                        String borrowdueinfo = (ass[0] + "*" + "BORROWED DATE: " + borrowDate + "*"  + "DUEDATE: " + dueDate + "*" + returncode + "*" + "\n");
			                        BorrowWriter.write(borrowdueinfo);
			                        BorrowWriter.close();
			                        
			                        //receipt
			                        System.out.println("---BORROW BOOOK RECEIPT---");
			                        System.out.println("Student ID: " + StudentID);
			                        System.out.println("Student Name: " + name);
			                        System.out.println("Book ID: " + ass[0]);
			                        System.out.println("Book Title: " + ass[2]);
			                        System.out.println("Book Author: " + ass[3]);
			                        System.out.println("Borrowed Date: " + borrowDate);
			                        System.out.println("Due date: " + dueDate);
			                        System.out.println("Your Return Code: " + returncode);
			                        returncode++;
			                       //for receipt need to write muna sa file yung borrow date and due date
			                        File receiptFile = new File("C:\\Users\\Kobe\\Downloads\\RECEIPT.txt");
			                        BufferedWriter ReceiptWriter = new BufferedWriter(new FileWriter(receiptFile, true));
			                        
			                        ReceiptWriter.write( "---BORROW BOOOK RECEIPT---" + "*" + " | " +
			    	                        "Student ID: " + StudentID + "*" + " | " +
			    	                        "Student Name: " + name + "*" + " | " +
			    	                        "Book ID" + ass[0] +  "*" + " | " +
			    	                        "Book Title: " + ass[2] +  "*" + " | " +
			    	                        "Book Author: " + ass[3] +  "*" + " | " +
			    	                        "Borrowed Date: " + borrowDate +  "*" + " | " +
			    	                        "Due date: " + dueDate +  "*" + " | " +
			    	                        "Your Return Code: " + returncode + "*") ;
			                        ReceiptWriter.write("\n"); // add extra newline to separate receipts
			                        
			                        ReceiptWriter.close();
			                        
			                        // Log borrow to UNAVAILABLEBOOKSOROUTSIDE.txt
			                    }else if(choice1.equalsIgnoreCase("N")) {
			                    	adminmenu();
			                    }
			                }
		               	}               		               
	                // Log borrow to UNAVAILABLEBOOKSOROUTSIDE.txt
      	            } else {
	                System.out.println("[Warning] Found corrupted record: " + link);
	            }
	            
	            String updatedLine = ass[0] + "*" + ass[1] + "*" + ass[2] + "*" + ass[3] + "*" + ass[4] + "*";
	            OriginalWriter.write(updatedLine + "\n");
	            //STUDENT LIMIT WRITER
	        }    Tempwriter.write(name + "*" + StudentID + "*" + Booktoborrow + "*" + limit +"*OUT\n");


	        Tempreaders.close();
	        OriginalWriter.close();
	        Tempwriter.close();
	        // Replace original book file with updated one
	  	        if (!found) {
	            System.out.println("Book not found");
	        }

	    } else {
	        System.out.println("INVALID STUDENT ID/NAME OR ACCOUNT DISABLED");
	        librarianmenu();
	    }
	}

	
	private static void returnbook() throws IOException {
		String status = "";

	    File inputFile = new File("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt");
        File tempFile = new File("C:\\Users\\Kobe\\Downloads\\OriginalBooks.txt.temp");
        
		BufferedReader reader = new BufferedReader(new FileReader(inputFile));
		
		   String parts;
		   System.out.println("---THESE ARE THE BOOKS CURRENTLY OUTSIDE---");
		    System.out.println("BookId |" + " Genre  |" + " Title |" + " Author |" + " Status");
		    while ((parts = reader.readLine()) != null) {
		        String[] arr = parts.split("\\*");
		        if (arr.length >= 5 &&  arr[4].equalsIgnoreCase("OUT")) {
		            System.out.println(arr[0] + " \t" + arr[1] + " \t " + arr[2] + " \t" + arr[3] + "\t" + arr[4]);
		        }
	}
		    reader.close();


		
		double totalPenalty = 0.00;
	    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
	    LocalDate today = LocalDate.now();
	   	
	BufferedReader Filereader = new BufferedReader(new FileReader(inputFile));
	BufferedWriter tempWriter = new BufferedWriter(new FileWriter(tempFile));
	String win;
	while((win = Filereader.readLine()) != null) {
		tempWriter.write(win +"\n");			//NALIPAT NA SA TEMP
	}
	
	Filereader.close();
	tempWriter.close();
	
	System.out.println("ENTER YOUR STUDENT NAME: ");
	String name = scan.next();
	
	System.out.println("ENTER THE BOOK ID TO RETURN:} ");
	String booktoreturn = scan.next();
	
	System.out.println("ENTER THE RETURN CODE: ");
	String bookreturncode = scan.next();
		
	BufferedReader Tempreader = new BufferedReader(new FileReader(tempFile));
	BufferedWriter FileWriter = new BufferedWriter(new FileWriter("C:\\\\Users\\\\Kobe\\\\Downloads\\\\OriginalBooks.txt"));//I REMOVE YUNG .temp
	
	
	boolean bookFound = false;
	String receiptContent = null; // Store receipt content for writing later

	String line;
	while ((line = Tempreader.readLine()) != null) {
	    String[] arr = line.split("\\*");
	    
	    if (booktoreturn.equals(arr[0])) {
	        if (arr.length >= 5 && "OUT".equalsIgnoreCase(arr[4])) {
	            // Process return
	            arr[4] = "AVAILABLE";
	            bookFound = true;		
	            
	            try (BufferedReader borrowreader = new BufferedReader(new FileReader("C:\\Users\\Kobe\\Downloads\\Borrow&Due.txt"))) {
	                String borrowLine;
	                while ((borrowLine = borrowreader.readLine()) != null) {
	                    String[] borrowData = borrowLine.split("\\*");
	                    if (bookreturncode.equals(borrowData[3]) && borrowData.length >= 3) {
	                        String dueDateStr = borrowData[2].substring(9, 19);
	                        LocalDate dueDate = LocalDate.parse(dueDateStr);
	                        
	                        if (today.isAfter(dueDate)) {
	                        	int daysLate = 0;
	                        	LocalDate current = dueDate.plusDays(1);
	                        	while (!current.isAfter(today)) {
	                        	    DayOfWeek day = current.getDayOfWeek();
	                        	    if (day != DayOfWeek.SATURDAY && day != DayOfWeek.SUNDAY) {
	                        	        daysLate++;
	                        	    }
	                        	    current = current.plusDays(1);
	                        	}
	                        	if (daysLate > 0) {
	                        	    totalPenalty = 100;
	                        	} else {
	                        	    totalPenalty = 0;
	                        	}
	                            System.out.println("The book is returned late. Penalty: " + totalPenalty);
	                        	decreaseBorrowCount(name);
	        	                logTransaction("Book " + arr[2] + " Returned late");
	                        } else if (today.isEqual(dueDate)) {
	                            System.out.println("The book is returned on the due date.");
	                        	decreaseBorrowCount(name);
	        	                logTransaction("Book " + arr[2] + " Returned on time");
	                        } else {
	                            System.out.println("The book is returned early.");
	                        	decreaseBorrowCount(name);
	        	                logTransaction("Book " + arr[2] + " Returned early");
	                        }
	                        break;
	                    }
	                }borrowreader.close();
	            }					       	
	            receiptContent = String.join("\n",
	                    "--- RETURN BOOK RECEIPT ---",
	                    "Book ID: " + arr[0],
	                    "Title: " + arr[2],
	                    "Author: " + arr[3],
	                    "Return Date: " + today,
	                    "Penalty: PHP " + totalPenalty,
	                    "THANK YOU FOR RETURNING",
	                    "------------------------"
	                );
	                
	                System.out.println("\n" + receiptContent);
	                if(totalPenalty > 0) {
	                	 File receiptFile = new File("C:\\Users\\Kobe\\Downloads\\RECEIPT.txt");
	                     BufferedReader ReceiptReader = new BufferedReader(new FileReader(receiptFile));
	                     
	                     String link;
	         	        while ((link = ReceiptReader.readLine()) != null) {
	         	            String[] parte = link.split("\\*");

	                	latefees(arr[2], totalPenalty);
	                }
	              }
	                
	              
	            } else {
	                System.out.println("This book is not currently checked out.");
	            }
	        
	        line = String.join("*", arr); // Update the line with new status

	    }
	    
	    FileWriter.write(line + "\n"); 
	    
	}if (receiptContent != null) {
	    try (BufferedWriter receiptWriter = new BufferedWriter( new FileWriter("C:\\Users\\Kobe\\Downloads\\RECEIPT.txt", true))) {
	        receiptWriter.write(receiptContent + "\n\n");
	        receiptWriter.close();
	    }
	}

	if (!bookFound) {
	    System.out.println("Invalid Book ID or book not checked out");
	}
			
	Tempreader.close();
	FileWriter.close();
}
	private static void latefees(String BookID, double totalPenalty ) {
		System.out.println("| Book Title \t |  " + "|Penalty|" );
		//gawa txt file name late fees
		
	}
	private static void logTransaction(String message) throws IOException {
		
		File log = new File("C:\\Users\\Kobe\\Downloads\\logTransaction.txt");
		BufferedWriter writer = new BufferedWriter(new FileWriter(log,true));
		LocalDate todayDate = LocalDate.now();
		
		writer.write(todayDate + " | " + message + " | " + "\n");
		writer.close();
	}
    private static void viewTransactions() throws IOException {

    	
    	File log = new File("C:\\Users\\Kobe\\Downloads\\logTransaction.txt");
    	BufferedReader reader = new BufferedReader(new FileReader(log));
		
		System.out.println("\n+------------------------------------------------------+");
        System.out.println("|📖 	Welcome to Transaction logs                          |");
        System.out.println("+--------------------------------------------------------+");
        System.out.println("| [1] View All Transactions                              |");
        System.out.println("| [2] View Transactions by Range                         |");
        System.out.println("| [3] View Transactions by Exact Date                    |");
        System.out.println("| [4] View Transactions by Week                          |");
        System.out.println("| [5] View All Monthly Transactions                      |");
        int choice = scan.nextInt();
        
		try{
		
		if(choice == 1) {
			String line;
			System.out.println("Date       |" + "Reports                           |");
			while((line = reader.readLine()) != null) {
				System.out.println(line);
				}
			
			reader.close();
			for(int i = 0; i < 2; i++) System.out.println();
			
		}else if(choice == 2) {
			System.out.println("USE THE FORMAT [YYYY-MM-DD] ");
			System.out.println("ENTER THE STARTING RANGE YOU WANT TO LOOK TO:  ");
			String Srange = scan.next();
			Srange.replace("-", "");
			
			System.out.println("ENTER THE END RANGE YOU WANT TO LOOK TO: ");
			String Erange = scan.next();
			Erange.replace("-", "");

			LocalDate startDate = LocalDate.parse(Srange);
			LocalDate endDate = LocalDate.parse(Erange);
			
			String line;
			System.out.println("Date       |" + "Reports                           |");
			while((line = reader.readLine()) != null) {
				String[] arr = line.split("\\|");
				try {
					
			        LocalDate logDate = LocalDate.parse(arr[0].trim());

			        if ((logDate.isEqual(startDate) || logDate.isAfter(startDate)) &&
			            (logDate.isEqual(endDate) || logDate.isBefore(endDate))) {

			            System.out.println(line);
			        }
			        
			    } catch (Exception e) {
			        System.out.println("Invalid date format in line: " + line);
			    }
			}
			for(int i = 0; i < 2; i++) System.out.println();
			
		}else if(choice == 3) {
			System.out.println("USE THE FORMAT [YYYY-MM-DD] ");
		    System.out.println("ENTER THE DATE YOU WANT TO CHECK [yyyy-MM-dd]: ");
			String Srange = scan.next();
			
			    try {
			        LocalDate targetDate = LocalDate.parse(Srange);

			        System.out.println("Date        | Reports");
			        
			        String line;
					while ((line = reader.readLine()) != null) {
			            String[] arr = line.split("\\|");

			            try {
			                LocalDate logDate = LocalDate.parse(arr[0].trim());

			                if (logDate.isEqual(targetDate)) {
			                    System.out.println(line);
			                }

			            } catch (Exception e) {
			                System.out.println("Invalid date format in line: " + line);
			            }
			        }

			    } catch (Exception e) {
			        System.out.println("Invalid date input format. Use yyyy-MM-dd");
			    }

			    reader.close();
				for(int i = 0; i < 2; i++) System.out.println();
				
		}else if(choice == 4) {
			System.out.println("ENTER THE STARTING DATE OF THE WEEK [yyyy-MM-dd]: ");
			String dateStr = scan.next();
			LocalDate weekStart = LocalDate.parse(dateStr);
			LocalDate weekEnd = weekStart.plusDays(6);
			
			System.out.println("Date        | Reports");
			
			String line;
			while ((line = reader.readLine()) != null) {
			    String[] arr = line.split("\\|");
			    try {
			        LocalDate logDate = LocalDate.parse(arr[0].trim());

			        if ((logDate.isEqual(weekStart) || logDate.isAfter(weekStart)) &&
			            (logDate.isEqual(weekEnd) || logDate.isBefore(weekEnd))) {
			            System.out.println(line);
			        }
			    } catch (Exception e) {
			        System.out.println("Invalid date format in line: " + line);
			    }
			}
			for(int i = 0; i < 2; i++) System.out.println();
			
		}else if(choice == 5) {
			System.out.println("ENTER THE YEAR AND MONTH YOU WANT TO CHECK [yyyy-MM]: ");
			String input = scan.next();
			YearMonth yearMonth = YearMonth.parse(input);
			LocalDate monthStart = yearMonth.atDay(1);
			LocalDate monthEnd = yearMonth.atEndOfMonth();
			
			System.out.println("Date        | Reports");
			
			String line;
			while ((line = reader.readLine()) != null) {
			    String[] arr = line.split("\\|");
			    try {
			        LocalDate logDate = LocalDate.parse(arr[0].trim());

			        if ((logDate.isEqual(monthStart) || logDate.isAfter(monthStart)) &&
			            (logDate.isEqual(monthEnd) || logDate.isBefore(monthEnd))) {
			            System.out.println(line);
			        }
			    } catch (Exception e) {
			        System.out.println("Invalid date format in line: " + line);
			    }
			}
			for(int i = 0; i < 2; i++) System.out.println();
			
		}else {
			System.out.println("invalid choice would you like to try again? [Y/N] ");
			String answer = scan.next().toLowerCase();
			
			switch(answer) {
			case "y":
				viewTransactions();
				break;
			case "n":
				adminmenu();
				break;
			}
		}
	}catch(Exception e) {
		System.out.println("Your input was invalid: " + e);
}
}public static void decreaseBorrowCount(String studentName) {
    File file = new File("C:\\Users\\Kobe\\Downloads\\UNAVAILABLEBOOKSOROUTSIDE.txt");
    ArrayList<String> updatedLines = new ArrayList<>();

    try {
        BufferedReader reader = new BufferedReader(new FileReader(file));
        String line;

        while ((line = reader.readLine()) != null) {
            String[] parts = line.split("\\*");

            if (parts.length >= 5 && parts[0].equalsIgnoreCase(studentName)) {
                int borrowCount = Integer.parseInt(parts[3]);
                if (borrowCount > 0) {
                    borrowCount--;
                    parts[3] = String.valueOf(borrowCount);
                    System.out.println("Borrow count for " + studentName + " decreased to " + borrowCount);
                }
            }

            // Rebuild and add the updated line to the list
            String updatedLine = String.join("*", parts);
            updatedLines.add(updatedLine);
        }

        reader.close();

        // Write updated lines back to the file
        BufferedWriter writer = new BufferedWriter(new FileWriter(file));
        for (String updatedLine : updatedLines) {
            writer.write(updatedLine);
            writer.newLine();
        }

        writer.close();

    } catch (IOException e) {
    	System.out.println(e);
    }
}

	private static void spacer() {
		for (int i = 0; i < 30; i++) {
			System.out.println();
		}
	}

	
	
	//EXTRA FILED(*) PARA MALAMAN IF ARCHIVE SYA OR NOT
}



