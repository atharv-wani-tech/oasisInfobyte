import java.util.*;

class ATM
{
    Scanner sc = new Scanner(System.in);
    double balance = 0; int i=1;
    double cname,acno,toa,dep,bal,witd;
    LinkedHashMap<Integer,String> stmt = new LinkedHashMap<Integer,String>();
    Map<Integer,Integer> cred = new TreeMap<>();
   
    ATM()   // constructor
    {
        System.out.println("...WELCOME TO ATM FACILITY...\n");
        
        cred.put(845710,5489); cred.put(547458,2145);
        cred.put(211548,8012); cred.put(457812,4541);
        cred.put(697015,8778); cred.put(210154,4870);
        
        System.out.print("Enter CUSTOMER ID : ");
        Integer id = sc.nextInt();
        Integer idchk = cred.get(id);
       
        if (cred.containsKey(id))
        {
            System.out.print("ENTER PIN : ");
            Integer pin = sc.nextInt();
            
            if ((idchk-pin)==0)
            {
                menu();
            }
            else
            {
                System.out.println("\nInvalid Pin!!!\nLast Chance to login\n\n");
                System.out.print("ENTER PIN : ");
                Integer pin1 = sc.nextInt();
                if ((idchk-pin1)==0)
                {
                    menu();
                }
                else
                {
                    System.out.println("\nInvalid Pin!!!\nMaximum limit Reached");
                    System.exit(0);
                }
            }
        }
        else
        {
            System.out.println("\nInvalid CUSTOMER ID!!!\nTry Again...");
            System.exit(0);
        }
        
    }
    
    public void menu()
    {
        System.out.println("SELECT YOUR CHOICE");
        System.out.println("1 MINI STATEMENT\t2 DEPOSIT\n3 ACCOUNT BALANCE\t4 WITHDRAWL\n5 CHANGE PIN\t\t6 EXIT");
        int choice = sc.nextInt();
        switch(choice)
        {
            case 1:
           // statement()
            { 
                System.out.println("Your account statement : \n");
                System.out.println("S.No.\tParticulars\t\tCredit\tDebit\tBalance");
                for(Integer key : stmt.keySet())
                {
                    System.out.println(key + stmt.get(key));
                }
                
                System.out.println("Redirected to main menu...\n");
                menu();
                break ;
            }
            case 2:
           // deposit()
            {
                System.out.println("Enter in multiple of 100 or 500 only!\n");
                System.out.print("Enter amount to deposit :");
                dep=sc.nextInt();
                if(dep%100==0)
                {
                bal=bal+dep;
                System.out.println("Amount deposited Successfully...\n");
                stmt.put(i,"\t Amount Deposited \t" + dep + "\t\t" + bal);
                i++;
                System.out.println("Redirected to main menu...\n");
                menu();
                break;
                }
                else
                {
                    System.out.println("WARNING!!\nEnter in multiple of 100 or 500 only!\n\n");
                    System.out.println("Press 1 to DEPOSIT\nPress 2 to Return Main Menu\n\nYour choice : ");
                    int choice1=sc.nextInt();
                    switch(choice1)
                    {
                    case 1:
                    {
                        System.out.print("Enter amount to deposit :");
                        dep=sc.nextInt();
                        if(dep%100==0)
                        {
                            bal=bal+dep;
                            System.out.println("Amount deposited Successfully...\n");
                            stmt.put(i,"\t Amount Deposited \t"+ dep + "\t\t" + bal);
                            i++;
                            System.out.println("Redirected to main menu...\n");
                            menu();
                            break;
                        }
                        else
                        {
                            System.out.println("Maximum attempts reached...Come back later!!\n\n");
                            System.out.println("Redirected to main menu...\n");
                            menu();
                            break;
                        }
                    }
                    case 2:
                    {
                        System.out.println("Redirected to main menu...\n");
                        menu();
                        break;
                    }
                    default :
                    {
                        System.out.println("Invalid input!!!\nRedirected to main menu...\n");
                        System.out.println("Redirected to main menu...\n");
                        menu();
                        break;
                    }
                    }    
                    
                }
            }
            case 3:
           // balance()
            {
                System.out.print("Your account balance is : "+bal+" Rs.\n\n");
                System.out.println("Redirected to main menu...\n");
                menu();
                break;
            }
            case 4:
           //withdrawl()
            {
                System.out.println("Available denomination : 100,200,500\n");
                System.out.print("Enter amount to withdraw :");
                witd=sc.nextInt();
               
                if (witd > bal)
                {
                    System.out.print("Insufficient balance!\n\n");
                    System.out.println("Redirected to main menu...\n");
                    menu();
                    break;
                }
                else
                {
                    if(witd%100==0)
                    {
                    bal=bal-witd;
                    System.out.print("Amount Withdrawl Successful\nPlease Collect your Cash!\n\n");
                    stmt.put(i,"\t Amount Withdrawl \t\t"+ witd + "\t" + bal);
                    i++;
                    System.out.println("Redirected to main menu...\n");
                    menu();
                    break;
                    }
                    else
                {
                    System.out.println("Invalid input!!!");
                    System.out.println("Available denomination : 100,200,500 only.\n");
                    System.out.print("Enter amount to withdraw :");
                witd=sc.nextInt();
                if (witd > bal)
                {
                    System.out.print("Insufficient balance!\n\n");
                    System.out.println("Redirected to main menu...\n");
                    menu();
                    break;
                }
                else
                {
                    if(witd%100==0)
                    {
                    bal=bal-witd;
                    System.out.print("Amount Withdrawl Successful\nPlease Collect your Cash!\n\n");
                    stmt.put(i,"\t Amount Withdrawl \t\t"+ witd + "\t" + bal);
                    i++;
                    System.out.println("Redirected to main menu...\n");
                    menu();
                    break;
                    }
                    else
                {
                    System.out.println("Maximum attempts reached...Come back later!!\n\n");
                    System.out.println("Redirected to main menu...\n");
                            menu();
                            break;
                }
                }
                }
                
                }
                
             
                
                
            }
            case 5:
           // changepin()
            {
                System.out.print("Enter CUSTOMER ID : ");
                Integer id = sc.nextInt();
                System.out.print("Enter New PIN : ");
                Integer npin = sc.nextInt();
                cred.put(id,npin);
                System.out.println("\nPin Changed Successfully!!!");
                System.out.println("\nRedirected to main menu...\n");
                menu();
                break;
            }
            case 6:
          //  exit()
            {
                 System.out.print("Thank you for banking with us!!!");
                 System.exit(0);
                 
            }
            default:
            {
                System.out.print("\nPlease Enter a Valid Choice(1/2/3/4/5/6)");
            }
            
        }
        
         
    }
}


public class Main
{
	public static void main(String[] args) 
	{
	    ATM a1 = new ATM();
	    
	}
}




        