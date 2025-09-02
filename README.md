# Calc

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SwingCalc extends JFrame implements ActionListener{ 

        JTextField tf;
        JButton[] funcButton = new JButton[8];
        JButton[] numButtons = new JButton[10];
        JButton addButton, subButton, divButton, mulButton, eqButton, clrButton, delButton, decButton;
        Panel panel;
        Font myFont = new Font("Courier New", Font.BOLD, 24);

        double num1, num2, result;
        char operator;

        SwingCalc() {

            // --- SET UP JFRAME
            setTitle("Calculator");
            setSize(450,650);
            setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            setLayout(null);


            // --- DESIGN LAYOUT ---
            panel = new Panel();
            panel.setLayout(new GridLayout(4, 4, 20, 20));
            panel.setBounds(50, 120, 300, 400);


            // --- INITIALIZE BUTTONS ---
            addButton = new JButton("+");
            subButton = new JButton("-");
            divButton = new JButton("/");
            mulButton = new JButton("*");
            eqButton = new JButton("=");
            delButton = new JButton("DEL");
            clrButton = new JButton("CLR");
            decButton = new JButton(".");

            funcButton[0] = addButton;
            funcButton[1] = subButton;
            funcButton[2] = divButton;
            funcButton[3] = mulButton;
            funcButton[4] = eqButton;
            funcButton[5] = delButton;
            funcButton[6] = decButton;
            funcButton[7] = clrButton;

            clrButton.setBounds(50, 550, 145, 50);
            delButton.setBounds(205, 550, 145, 50);

            for(int i=0;i<10;i++)
            {
                numButtons[i] = new JButton(String.valueOf(i));
                numButtons[i].setFont(myFont);
                numButtons[i].setFocusable(false);
                numButtons[i].addActionListener(this);
            }

            for(int j=0;j<8;j++)
            {
                funcButton[j].setFont(myFont);
                funcButton[j].setFocusable(false);
                funcButton[j].addActionListener(this);
            }

            // --- DISPLAY TEXT-FIELD ---
            tf = new JTextField();
            tf.setEditable(false);
            tf.setBounds(50, 25, 330, 60);
            tf.setFont(myFont);

            // --- ADD ---
            add(tf);
            add(panel);
            panel.add(numButtons[1]);
            panel.add(numButtons[2]);
            panel.add(numButtons[3]);
            panel.add(addButton);
            panel.add(numButtons[4]);
            panel.add(numButtons[5]);
            panel.add(numButtons[6]);
            panel.add(subButton);
            panel.add(numButtons[7]);
            panel.add(numButtons[8]);
            panel.add(numButtons[9]);
            panel.add(mulButton);
            panel.add(divButton);
            panel.add(decButton);
            panel.add(numButtons[0]);
            panel.add(eqButton);
            
            add(clrButton);
            add(delButton);

            setVisible(true);
        }

    public void actionPerformed(ActionEvent ae) {

        for(int i=0;i<10;i++)
        {
            if (ae.getSource() == numButtons[i]) {
                tf.setText(tf.getText().concat(String.valueOf(i)));
            }
        }

        if (ae.getSource() == decButton) {
            tf.setText(tf.getText().concat("."));
        }

        if (ae.getSource() == addButton) {
            num1 = Double.parseDouble(tf.getText());
            operator = '+';
            tf.setText("");
        }

        if (ae.getSource() == subButton) {
            num1 = Double.parseDouble(tf.getText());
            tf.setText("");
            operator = '-';
        }

        if (ae.getSource() == divButton) {
            num1 = Double.parseDouble(tf.getText());
            tf.setText("");
            operator = '/';
        }

        if (ae.getSource() == mulButton) {
            num1 = Double.parseDouble(tf.getText());
            tf.setText("");
            operator = '*';
        }

        if (ae.getSource() == eqButton) {
            num2 = Double.parseDouble(tf.getText());

            switch (operator) {
                case '+':
                    result = num1+num2;
                    break;
                case '-':
                    result = num1-num2;
                    break;
                case '*':
                    result = num1*num2;
                    break;
                case '/':
                    if (num2==0) {
                        tf.setText("Error!");
                    } else {
                        result = num1/num2;
                    }
                    break;
                
                default:
                    break;
            }
            tf.setText(result+"");
        }

        if (ae.getSource() == clrButton) {
            tf.setText("");
            num1 = num2 = result = 0;
        }

        if (ae.getSource() == delButton) {
            String currString = tf.getText();

            if (!currString.isEmpty()) {
                tf.setText(currString.substring(0, currString.length()-1));
            }
        }
    }

    public static void main(String[] args) {
        SwingCalc c = new SwingCalc(); 

    }
}

#Output:

<img width="435" height="635" alt="image" src="https://github.com/user-attachments/assets/0d3f14ab-d1a6-46c6-adcb-f88ca02c1a09" />
