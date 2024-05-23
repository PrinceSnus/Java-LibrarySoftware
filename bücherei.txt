import javax.swing.*;
import java.util.*;
import java.awt.*;
import java.awt.event.*;
public class Datenbank extends JFrame implements ActionListener {
    private JLabel label1, label2, label3, label4, label5, label6, label7; //Die Texte links neben den Textfeldern
    private JTextField textField1, textField2, textField3, textField4, textField5, textField6, textField7; //Die eigentlichen Textfeldern wo Daten eingetragen werden
    private JButton hinzKnopf, ansiKnopf, löschKnopf, endeKnopf; // Die Knöpfe die eine Aktion ausführen
    private JPanel panel;
    private ArrayList<String[]> buecher = new ArrayList<String[]>();
    public Datenbank() {
        setTitle("Bücher-Datenbank");
        setSize(320, 240);
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        label1 = new JLabel("Bücher ID");
        label2 = new JLabel("Buchtitel");
        label3 = new JLabel("Autor");
        label4 = new JLabel("Verlag");
        label5 = new JLabel("Veröffentlichungsdatum");
        label6 = new JLabel("ISBN-Nummer");
        label7 = new JLabel("Anzahl der Bücher");

        textField1 = new JTextField(50);
        textField2 = new JTextField(50);
        textField3 = new JTextField(50);
        textField4 = new JTextField(50);
        textField5 = new JTextField(50);
        textField6 = new JTextField(50);
        textField7 = new JTextField(50);

        hinzKnopf = new JButton("Hinzufügen");
        ansiKnopf = new JButton("Ansicht/Bearbeiten");
        löschKnopf = new JButton("Löschen");
        endeKnopf = new JButton("Beenden");

        hinzKnopf.addActionListener(this);
        ansiKnopf.addActionListener(this);
        löschKnopf.addActionListener(this);
        endeKnopf.addActionListener(this);

        panel = new JPanel(new GridLayout(9,2));
        panel.add(label1);
        panel.add(textField1);
        panel.add(label2);
        panel.add(textField2);
        panel.add(label3);
        panel.add(textField3);
        panel.add(label4);
        panel.add(textField4);
        panel.add(label5);
        panel.add(textField5);
        panel.add(label6);
        panel.add(textField6);
        panel.add(label7);
        panel.add(textField7);

        panel.add(hinzKnopf);
        panel.add(ansiKnopf);
        panel.add(löschKnopf);
        panel.add(endeKnopf);

        add(panel);

        setVisible(true);
    }

    public void actionPerformed(ActionEvent a) {
        if (a.getSource() == hinzKnopf) {
            String[] buch = new String[7];
            buch[0] = textField1.getText();
            buch[1] = textField2.getText();
            buch[2] = textField3.getText();
            buch[3] = textField4.getText();
            buch[4] = textField5.getText();
            buch[5] = textField6.getText();
            buch[6] = textField7.getText();
            buecher.add(buch);
            JOptionPane.showMessageDialog(this, "Buch erfolgreich hinzugefügt!");
            TextfeldLeeren();
        }
        else if (a.getSource() == ansiKnopf) {
            String[] columns = {"Bücher ID", "Buchtitel", "Autor", "Verlag", "Veröffentlichungsdatum", "ISBN-Nummer", "Anzahl der Bücher"};
            Object[][] data = new Object[buecher.size()][7];
            for (int i = 0; i < buecher.size(); i++) {
                data[i][0] = buecher.get(i)[0];
                data[i][1] = buecher.get(i)[1];
                data[i][2] = buecher.get(i)[2];
                data[i][3] = buecher.get(i)[3];
                data[i][4] = buecher.get(i)[4];
                data[i][5] = buecher.get(i)[5];
                data[i][6] = buecher.get(i)[6];
            }
            JTable table = new JTable(data, columns);
            JScrollPane scrollPane = new JScrollPane(table);
            JFrame frame = new JFrame("Bücher ansehen und bearbeiten");
            frame.add(scrollPane);
            frame.setSize(800, 240);
            frame.setVisible(true);
        }
        else if (a.getSource() == löschKnopf) {
            String buchID = JOptionPane.showInputDialog(this, "Bücher ID eingeben zum entfernen:");
            for (int i = 0; i < buecher.size(); i++) {
                if (buecher.get(i)[0].equals(buchID)) {
                    buecher.remove(i);
                    JOptionPane.showMessageDialog(this, "Buch erfolgreich entfernt!");
                    TextfeldLeeren();
                    return;
                }
            }
            JOptionPane.showMessageDialog(this, "Buch nicht gefunden");
        }
        else if (a.getSource() == endeKnopf) {
            System.exit(0);
        }
    }

    private void TextfeldLeeren() {
        textField1.setText("");
        textField2.setText("");
        textField3.setText("");
        textField4.setText("");
        textField5.setText("");
        textField6.setText("");
        textField7.setText("");
    }

    public static void main(String[] args) {
        new Datenbank();
    }
}