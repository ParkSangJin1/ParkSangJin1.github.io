---
layout: single
title: "TeamProject-VendingMachine"
date: 2020-04-26 18:12:12 +0900
---

# 팀 프로젝트 - 자판기



## 조원/파트

__신은섭 - case 1 알고리즘 담당__

__혁연휘 - case 2 알고리즘 담당__

__박상진 - GUI, Swing 담당__



## Vending Machine

- #### 자바 Swing GUI 이용

- #### JFrame으로 프레임 생성 후, JSpinner, JLabel, JTextField 등을 이용하여 디자인

- #### JButton에 ImageIcon 함수 이용해 이미지 삽입

- #### ActionListener로 총액 합산 출력(스피너 값 확정 후 계산)과 거스름돈 동전 개수를 나타내는 팝업창을 띄우도록 설정

- #### Case 1은 동적알고리즘, Case 2는 그리디 알고리즘을 통해서 계산할 수 있도록 설계



## 코드

~~~java
import java.awt.*;
import javax.swing.*;
import javax.swing.event.*;
import java.awt.event.*;

class countChange extends JFrame {
	
	static JFrame sbfr = new JFrame();
	
	public static int DpCoinChange(int money) {
	       
		  int coin[] = {10000, 5000, 1600, 1000, 500, 100, 10, 1};
	      int c[]=new int[money+1];
	      
	       int i,j,k;
	      
	       int[][] coinNum=new int[money+1][coin.length];
	       
	       for(i=0;i<=money;i++) {
	          c[i]=9999999;
	          for(j=0;j<coin.length;j++)
	             coinNum[i][j]=0;
	       }
	       c[0]=0;
	       
	       
	       for(j=1;j<=money;j++) {
	          for(i=0;i<coin.length;i++) {
	             if((coin[i]<=j)&&(c[j-coin[i]]+1<c[j])) {
	                for(k=0;k<coin.length;k++)
	                   coinNum[j][k]=coinNum[j-coin[i]][k];
	                coinNum[j][i]++;
	                c[j]=c[j-coin[i]]+1;
	          }
	       }
	       }
	       
	       int tot1 = 0;
	         
	         for (i=0; i<coin.length; i++) {
	     		JTextField tfnum2 = new JTextField(coinNum[money][i]+"개");
	     		tfnum2.setHorizontalAlignment(JTextField.RIGHT);
	     		tfnum2.setBounds(200, 60+(35*i), 80, 25);
	     		sbfr.add(tfnum2);
	     		tot1 += coinNum[money][i];
	         }
	       
	        return tot1;
	   }
	
	countChange(int change) {
		
		sbfr.setTitle("거스름돈 계산하기");
		sbfr.setLayout(null);
		sbfr.setSize(500,400);
		sbfr.setVisible(true);
		
		
		//
		
		int coin[] = {10000, 5000, 1600, 1000, 500, 100, 10, 1};
		
		for (int i=0; i<coin.length; i++) {
        	JLabel lbcoin = new JLabel(coin[i]+"원");
        	lbcoin.setHorizontalAlignment(JTextField.RIGHT);
        	lbcoin.setBounds(10, 60+(35*i), 80, 25);
        	sbfr.add(lbcoin);
        }
        
        JLabel total = new JLabel("총 동전의 개수");
        total.setBounds(17, 340, 80, 25);
        sbfr.add(total);
        
        // case 1
        
        JLabel case1 = new JLabel("[CASE 1]");
        case1.setBounds(213,10,100,50);
        sbfr.add(case1);
       
        DpCoinChange(change);
        
        JTextField tftot1 = new JTextField(DpCoinChange(change)+"개"); // case 2의 동전의 총 개수
        tftot1.setHorizontalAlignment(JTextField.RIGHT);
        tftot1.setBounds(200, 340, 80, 25);
        sbfr.add(tftot1);
        
        // case 2
        
        JLabel case2 = new JLabel("[CASE 2]");
        case2.setBounds(363,10,100,50);
        sbfr.add(case2);
        
        int[] n= new int[coin.length];
        int tot2 = 0;
        
        for(int i=0;i<coin.length;i++)
           n[i]=0;
        
        for(int i=0;i<coin.length;i++) {
           while(change >= coin[i]) {
              change-=coin[i];
              n[i]++;
           }
        }
        
        for (int i=0; i<coin.length; i++) {
        		JTextField tfnum1 = new JTextField(n[i]+"개");
        		tfnum1.setHorizontalAlignment(JTextField.RIGHT);
        		tfnum1.setBounds(350, 60+(35*i), 80, 25);
        		sbfr.add(tfnum1);
        		tot2 += n[i];
        	}
        
        JTextField tftot2 = new JTextField(tot2+"개"); // case 1의 동전의 총 개수
        tftot2.setHorizontalAlignment(JTextField.RIGHT);
        tftot2.setBounds(350, 340, 80, 25);
        sbfr.add(tftot2);
        }
	}

public class Frame {
   
   public static void main(String[] args) {
      
      JFrame fr = new JFrame();
      fr.setTitle("VendingMachine");
      fr.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
      fr.setLayout(null);
      fr.setBackground(Color.white);
      
      JTextField tf1 = new JTextField("낼 금액을 입력 해주세요.");
      tf1.setHorizontalAlignment(JTextField.RIGHT);
      tf1.setEditable(true);
      tf1.setBounds(290, 300, 160, 20);
      fr.add(tf1);
      
      JLabel lbwon1 = new JLabel("원");
      lbwon1.setBounds(450, 260, 100, 100);
      fr.add(lbwon1);
      
      JButton b1 = new JButton("총 금액");
      b1.setBounds(290, 270, 80, 20);
      fr.add(b1);
      
      JTextField tf2 = new JTextField("");
      tf2.setHorizontalAlignment(JTextField.RIGHT);
      tf2.setEditable(false);
      tf2.setBounds(380, 270, 70, 20);
      fr.add(tf2);
      
      JLabel lbwon2 = new JLabel("원");
      lbwon2.setBounds(450, 230, 100, 100);
      fr.add(lbwon2);
      
      JButton b2 = new JButton("거스름 돈 계산하기");
      b2.setBounds(290, 330, 170, 20);
      fr.add(b2);
      
      JLabel warning = new JLabel("$$ 0개 이하 선택시 0개로 계산됩니다. $$");
      warning.setBounds(150,130,250,200);
      fr.add(warning);
      
      //
      int price[] = {3500, 1500, 4000};
      int value[] = new int[3];
      
      JLabel lb1 = new JLabel("[라면 - 3500원]");
      lb1.setBounds(50,100,100,100);
      fr.add(lb1);
      
      JButton bram = new JButton(new ImageIcon("src/images/라면.jpg"));
      bram.setBounds(50, 30, 90, 90);
      fr.add(bram);
      
      JSpinner spram = new JSpinner();
      spram.setBounds(60, 170, 80, 20);
      fr.add(spram);
      
      // 라면   
      
      JLabel lb2 = new JLabel("[콜라 - 1500원]");
      lb2.setBounds(210,100,100,100);
      fr.add(lb2);
      
      JButton bcol = new JButton(new ImageIcon("src/images/콜라.jpg"));
      bcol.setBounds(210, 30, 90, 90);
      fr.add(bcol);
      
      JSpinner spcol = new JSpinner();
      spcol.setBounds(220, 170, 80, 20);
      fr.add(spcol);
      
      // 콜라    
      
      JLabel lb3 = new JLabel("[햄버거 - 4000원]");
      lb3.setBounds(350,100,100,100);
      fr.add(lb3);
      
      
      JButton bham = new JButton(new ImageIcon("src/images/햄버거.jpg"));
      bham.setBounds(350, 30, 90, 90);
      fr.add(bham);
      
      JSpinner spham = new JSpinner();
      spham.setBounds(360, 170, 80, 20);
      fr.add(spham);
      
      // 햄버거  

      fr.setSize(500,400);
      fr.setVisible(true);
      
   // 총 금액 이벤트 처리
    b1.addActionListener(new ActionListener() {
          
        @Override
   
        public void actionPerformed(ActionEvent e) {
          
           value[0] = (int) spram.getValue();
           value[1] = (int) spcol.getValue();
           value[2] = (int) spham.getValue();
           
           int result = 0;
           
          for (int i=0; i<3; i++) {
             if (value[i] < 0)
                value[i] = 0;
           result += value[i] * price[i];
          }
            tf2.setText(""+result); // 합계 출력
        }
        });
    b2.addActionListener(new ActionListener() {
        
        @Override
   
        public void actionPerformed(ActionEvent e) {
        	
        	String money = tf1.getText(); // 입력한 금액
        	String sum = tf2.getText(); // 상품 총 금액
        	
        	int a = Integer.parseInt(money);
        	int b = Integer.parseInt(sum);
        	
        	if (a < 0)
        		return;
        	if (b < 0)
        		return;
        	
        	int change = a - b;
           
        	new countChange(change);
        }
        });
}
}
~~~



## 실행 결과

![스크린샷 2020-04-26 오후 6.07.01](/Users/Juhee/Desktop/스크린샷 2020-04-26 오후 6.07.01.png)



스피너로 각 음식의 수량 설정 후, 총 금액 버튼을 누르면 오른쪽 텍스트 필드에 총액이 나타난다.

바로 밑의 텍스트 필드에 낼 금액을 입력 하고, 거스름 돈 계산하기 버튼을 클릭하면 오른쪽의 팝업창이 뜬다.

case 1은 동적 알고리즘을 이용했을 때의 동전 개수이고, case 2는 그리디 알고리즘을 이용했을 때의 동전 개수이다.