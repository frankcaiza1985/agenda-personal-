import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;
import java.awt.event.*;
import java.text.SimpleDateFormat;
import java.util.Date;

public class AgendaPersonal extends JFrame {

    // Componentes de entrada
    private JSpinner spinnerFecha;
    private JSpinner spinnerHora;
    private JTextField txtDescripcion;

    // Tabla y modelo
    private JTable tablaEventos;
    private DefaultTableModel modeloTabla;

    // Botones
    private JButton btnAgregar;
    private JButton btnEliminar;
    private JButton btnSalir;

    public AgendaPersonal() {
        setTitle("Agenda Personal");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(600, 400);
        setLocationRelativeTo(null);

        // Panel principal con BorderLayout
        setLayout(new BorderLayout(10, 10));

        // ---------- PANEL SUPERIOR (Entrada de datos) ----------
        JPanel panelEntrada = new JPanel(new GridLayout(3, 2, 5, 5));

        // Fecha
        panelEntrada.add(new JLabel("Fecha (dd/MM/yyyy):"));
        spinnerFecha = new JSpinner(new SpinnerDateModel());
        spinnerFecha.setEditor(new JSpinner.DateEditor(spinnerFecha, "dd/MM/yyyy"));
        panelEntrada.add(spinnerFecha);

        // Hora
        panelEntrada.add(new JLabel("Hora (HH:mm):"));
        spinnerHora = new JSpinner(new SpinnerDateModel());
        spinnerHora.setEditor(new JSpinner.DateEditor(spinnerHora, "HH:mm"));
        panelEntrada.add(spinnerHora);

        // Descripción
        panelEntrada.add(new JLabel("Descripción:"));
        txtDescripcion = new JTextField();
        panelEntrada.add(txtDescripcion);

        add(panelEntrada, BorderLayout.NORTH);

        // ---------- PANEL CENTRAL (Tabla de eventos) ----------
        modeloTabla = new DefaultTableModel(new Object[]{"Fecha", "Hora", "Descripción"}, 0);
        tablaEventos = new JTable(modeloTabla);
        JScrollPane scrollPane = new JScrollPane(tablaEventos);

        add(scrollPane, BorderLayout.CENTER);

        // ---------- PANEL INFERIOR (Botones) ----------
        JPanel panelBotones = new JPanel(new FlowLayout(FlowLayout.CENTER, 15, 10));

        btnAgregar = new JButton("Agregar");
        btnEliminar = new JButton("Eliminar seleccionado");
        btnSalir = new JButton("Salir");

        panelBotones.add(btnAgregar);
        panelBotones.add(btnEliminar);
        panelBotones.add(btnSalir);

        add(panelBotones, BorderLayout.SOUTH);

        // ---------- MANEJO DE EVENTOS ----------
        btnAgregar.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                agregarEvento();
            }
        });

        btnEliminar.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                eliminarEvento();
            }
        });

        btnSalir.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                dispose(); // cerrar ventana
            }
        });
    }

    // Método para agregar evento
    private void agregarEvento() {
        String descripcion = txtDescripcion.getText().trim();

        if (descripcion.isEmpty()) {
            JOptionPane.showMessageDialog(this,
                    "La descripción no puede estar vacía",
                    "Validación",
                    JOptionPane.WARNING_MESSAGE);
            return;
        }

        Date fecha = (Date) spinnerFecha.getValue();
        Date hora = (Date) spinnerHora.getValue();

        SimpleDateFormat sdfFecha = new SimpleDateFormat("dd/MM/yyyy");
        SimpleDateFormat sdfHora = new SimpleDateFormat("HH:mm");

        String fechaStr = sdfFecha.format(fecha);
        String horaStr = sdfHora.format(hora);

        modeloTabla.addRow(new Object[]{fechaStr, horaStr, descripcion});

        // Limpiar campo descripción
        txtDescripcion.setText("");
        txtDescripcion.requestFocus();
    }

    // Método para eliminar evento
    private void eliminarEvento() {
        int filaSeleccionada = tablaEventos.getSelectedRow();

        if (filaSeleccionada == -1) {
            JOptionPane.showMessageDialog(this,
                    "Selecciona un evento primero",
                    "Aviso",
                    JOptionPane.WARNING_MESSAGE);
            return;
        }

        int confirmacion = JOptionPane.showConfirmDialog(this,
                "¿Eliminar el evento seleccionado?",
                "Confirmar eliminación",
                JOptionPane.YES_NO_OPTION);

        if (confirmacion == JOptionPane.YES_OPTION) {
            modeloTabla.removeRow(filaSeleccionada);
        }
    }

    // Método principal
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            new AgendaPersonal().setVisible(true);
        });
    }
}
