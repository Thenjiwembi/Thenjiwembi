- 👋 Hi, I’m @Thenjiwembi
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Thenjiwembi/Thenjiwembi is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
public class SubjectApplicationGUI extends JFrame {
    private JTextField subjectCodeTextField;
    private JTextField subjectNameTextField;
    private JButton addButton;
    private JButton listButton;
    private JTable subjectTable;
    private SubjectTableModel tableModel;

    public SubjectApplicationGUI() {
        initializeComponents();
        addComponentsToFrame();
    }

    private void initializeComponents() {
        subjectCodeTextField = new JTextField(10);
        subjectNameTextField = new JTextField(20);
        addButton = new JButton("Add");
        listButton = new JButton("List");
        subjectTable = new JTable();
        subjectTable.setPreferredSize(new Dimension(400, 200));

        addButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                addSubject();
            }
        });

        listButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                listSubjects();
            }
        });

        tableModel = new SubjectTableModel();
        subjectTable.setModel(tableModel);
    }

    private void addComponentsToFrame() {
        JPanel panel = new JPanel();
        panel.add(new JLabel("Subject Code:"));
        panel.add(subjectCodeTextField);
        panel.add(new JLabel("Subject Name:"));
        panel.add(subjectNameTextField);
        panel.add(addButton);
        panel.add(listButton);

        setLayout(new FlowLayout());
        add(panel);
        add(new JScrollPane(subjectTable));

        setTitle("Subject Application");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        pack();
        setLocationRelativeTo(null);
        setVisible(true);
    }

    private void addSubject() {
        String subjectCode = subjectCodeTextField.getText();
        String subjectName = subjectNameTextField.getText();

        Subject subject = new Subject();
        subject.setSubjectCode(subjectCode);
        subject.setSubjectName(subjectName);

        try {
            SubjectDAO.addSubject(subject);
            JOptionPane.showMessageDialog(this, "Subject added successfully");
            clearFields();
        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(this, "Error adding subject: " + ex.getMessage(), "Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    private void listSubjects() {
        try {
            List<Subject> subjects = SubjectDAO.getAllSubjects();
            tableModel.setSubjects(subjects);
        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(this, "Error listing subjects: " + ex.getMessage(), "Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    private void clearFields() {
        subjectCodeTextField.setText("");
        subjectNameTextField.setText("");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new SubjectApplicationGUI();
            }
        });
    }
}
public class SubjectTableModel extends AbstractTableModel {
    private List<Subject> subjects;
    private final String[] columnNames = {"Subject Code", "Subject Name"};

    public void setSubjects(List<Subject> subjects) {
        this.subjects = subjects;
        fireTableDataChanged();
    }

    @Override
    public int getRowCount() {
        if (subjects != null) {
            return subjects.size();
        }
        return 0;
    }

    @Override
    public int getColumnCount() {
        return columnNames.length;
    }

    @Override
    public Object getValueAt(int rowIndex, int columnIndex) {
        Subject subject = subjects.get(rowIndex);
        if (columnIndex == 0) {
            return subject.getSubjectCode();
        } else if (columnIndex == 1) {
            return subject.getSubjectName();
        }
        return null;
    }

    @Override
    public String getColumnName(int column) {
        return columnNames[column];
    }
}
public class SubjectTableModel extends AbstractTableModel {
    private List<Subject> subjects;
    private final String[] columnNames = {"Subject Code", "Subject Name"};

    public void setSubjects(List<Subject> subjects) {
        this.subjects = subjects;
        fireTableDataChanged();
    }

    @Override
    public int getRowCount() {
        if (subjects != null) {
            return subjects.size();
        }
        return 0;
    }

    @Override
    public int getColumnCount() {
        return columnNames.length;
    }

    @Override
    public Object getValueAt(int rowIndex, int columnIndex) {
        Subject subject = subjects.get(rowIndex);
        if (columnIndex == 0) {
            return subject.getSubjectCode();
        } else if (columnIndex == 1) {
            return subject.getSubjectName();
        }
        return null;
    }

    @Override
    public String getColumnName(int column) {
        return columnNames[column];
    }
}

public class SubjectTableModel extends AbstractTableModel {
    private List<Subject> subjects;
    private final String[] columnNames = {"Subject Code", "Subject Name"};

    public void setSubjects(List<Subject> subjects) {
        this.subjects = subjects;
        fireTableDataChanged();
    }

    @Override
    public int getRowCount() {
        if (subjects != null) {
            return subjects.size();
        }
        return 0;
    }

    @Override
    public int getColumnCount() {
        return columnNames.length;
    }

    @Override
    public Object getValueAt(int rowIndex, int columnIndex) {
        Subject subject = subjects.get(rowIndex);
        if (columnIndex == 0) {
            return subject.getSubjectCode();
        } else if (columnIndex == 1) {
            return subject.getSubjectName();
        }
        return null;
    }

    @Override
    public String getColumnName(int column) {
        return columnNames[column];
    }
}

