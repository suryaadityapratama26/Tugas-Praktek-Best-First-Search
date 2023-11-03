﻿Nama : Surya Aditya Pratama (5311421026)

Praktek Best First Search

(Tic Tac Toe)

package TicTacToe;

/\*\* \* Enumeration for the various states of the game \*/ public enum

GameState { // to save as "GameState.java"

PLAYING, DRAW, CROSS\_WON, NOUGHT\_WON

}

- ` `**GameState** (dalam **GameState.java**):

Ini adalah enumerasi yang digunakan untuk mewakili status permainan Tic-Tac-Toe. Ada empat nilai yang mungkin:

1. **PLAYING**: Ini menunjukkan bahwa permainan masih berlangsung.
1. **DRAW**: Ini menunjukkan bahwa permainan berakhir dengan hasil imbang (tidak ada pemain yang menang).
1. **CROSS\_WON**: Ini menunjukkan bahwa pemain yang menggunakan tanda "X" telah menang.
1. **NOUGHT\_WON**: Ini menunjukkan bahwa pemain yang menggunakan tanda "O" telah menang.


package TicTacToe;

/\*\* \* Enumeration for the seeds and cell contents \*/ public enum Seed {

// to save as "Seed.java"

EMPTY, CROSS, NOUGHT

}

- **Seed** (dalam **Seed.java**):
1. Ini adalah enumerasi yang digunakan untuk merepresentasikan isi sel pada papan permainan. Ada tiga nilai yang mungkin:
1. **EMPTY**: Ini menunjukkan bahwa sel di papan permainan masih kosong.
1. **CROSS**: Ini menunjukkan bahwa sel diisi dengan tanda "X".
1. **NOUGHT**: Ini menunjukkan bahwa sel diisi dengan tanda "O".










package TicTacToe;

/\*\* \* Enumeration for the various states of the game \*/ public enum

State { // to save as "GameState.java"

PLAYING, DRAW, CROSS\_WON, NOUGHT\_WON

}

- **State** (dalam **GameState.java**):

Ini adalah enumerasi yang terlihat serupa dengan **GameState**, tetapi mungkin merupakan duplikasi. Pada dasarnya, enumerasi ini juga digunakan untuk mewakili status permainan Tic-Tac-Toe dan memiliki nilai yang sama seperti **PLAYING**, **DRAW**, **CROSS\_WON**, dan **NOUGHT\_WON**. Namun, menciptakan duplikasi enumerasi mungkin merupakan kesalahan penulisan yang harus dihindari.






























package TicTacToe;

import java.awt.Graphics;

import java.awt.\*;

import java.awt.Graphics2D;

public class Cell {

//content of this cell (Seed.EMPTY, Seed.CROSS, or Seed.NOUGHT)

` `Seed content;

` `int row, col; // row and column of this cell

/\*\*Constructor to initialize this cell with the specified row and col \*/

` `public Cell(int row, int col) {

` `this.row = row;

` `this.col = col;

` `clear(); // clear content

` `}

` `/\*\* Clear this cell's content to EMPTY \*/

` `public void clear() {

` `content = Seed.EMPTY;

` `}

` `/\*\*Paint itself on the graphics canvas, given the Graphics context \*/

` `public void paint(Graphics g) {

` `// Use Graphics2D which allows us to set the pen's stroke

` `Graphics2D g2d = (Graphics2D)g;

` `g2d.setStroke(new BasicStroke(GameMain.SYMBOL\_STROKE\_WIDTH,

` `BasicStroke.CAP\_ROUND, BasicStroke.JOIN\_ROUND)); // Graphics2Donly

` `// Draw the Seed if it is not empty

` `int x1 = col \* GameMain.CELL\_SIZE + GameMain.CELL\_PADDING;

` `int y1 = row \* GameMain.CELL\_SIZE + GameMain.CELL\_PADDING;

` `if (content == Seed.CROSS) {

` `g2d.setColor(Color.RED);

` `int x2 = (col + 1) \* GameMain.CELL\_SIZE - GameMain.CELL\_PADDING;

` `int y2 = (row + 1) \* GameMain.CELL\_SIZE - GameMain.CELL\_PADDING;

` `g2d.drawLine(x1, y1, x2, y2);

` `g2d.drawLine(x2, y1, x1, y2);

` `} else if (content == Seed.NOUGHT) {

` `g2d.setColor(Color.BLUE);

` `g2d.drawOval(x1, y1, GameMain.SYMBOL\_SIZE, GameMain.SYMBOL\_SIZE);

` `}

` `}

}


Kode ini merupakan bagian dari permainan Tic-Tac-Toe yang lebih besar yang mungkin mencakup kelas-kelas dan logika lain untuk mengatur permainan. Kelas **Cell** ini bertanggung jawab untuk menggambar dan mengatur isi setiap sel pada papan permainan.

- **Seed content**: Ini adalah atribut yang merepresentasikan isi dari sel tersebut. Nilai dari **Seed** bisa berupa **EMPTY**, **CROSS**, atau **NOUGHT** sesuai dengan apakah sel tersebut kosong atau diisi dengan tanda "X" atau "O".
- **int row, col**: Ini adalah atribut yang menyimpan posisi baris dan kolom dari sel tersebut di papan permainan.
- Konstruktor **Cell(int row, int col)**: Konstruktor ini digunakan untuk membuat objek **Cell** dengan baris dan kolom tertentu. Saat objek **Cell** dibuat, isi selnya diatur ke **EMPTY** menggunakan metode **clear()**.
- Metode **clear()**: Metode ini digunakan untuk menghapus isi sel dan mengaturnya kembali ke **EMPTY**.
- Metode **paint(Graphics g)**: Metode ini digunakan untuk menggambar sel pada papan permainan. Ini memanfaatkan objek **Graphics** untuk menggambar tanda "X" (dengan warna merah) atau "O" (dengan warna biru) di sel tersebut. Penggambaran tanda "X" dilakukan dengan menggambar dua garis silang, sementara penggambaran tanda "O" dilakukan dengan menggambar oval.



























package TicTacToe;

import java.awt.\*;

/\*\*

\* The Board class models the ROWS-by-COLS game-board.

\*/

public class Board {

` `// package access

` `// composes of 2D array of ROWS-by-COLS Cell instances

` `Cell[][] cells;

` `/\*\* Constructor to initialize the game board \*/

` `public Board() {

// allocate the array

` `cells = new Cell[GameMain.ROWS][GameMain.COLS];

` `for (int row = 0; row < GameMain.ROWS; ++row) {

` `for (int col = 0; col < GameMain.COLS; ++col) {

` `// allocate element of array

` `cells[row][col] = new Cell(row, col);

` `}

` `}

` `}

` `/\*\* Initialize (or re-initialize) the game board \*/

` `public void init() {

` `for (int row = 0; row < GameMain.ROWS; ++row) {

` `for (int col = 0; col < GameMain.COLS; ++col) {

` `// clear the cell content

` `cells[row][col].clear();

` `}

` `}

` `}

` `/\*\* Return true if it is a draw (i.e., no more EMPTY cell) \*/

` `public boolean isDraw() {

` `for (int row = 0; row < GameMain.ROWS; ++row) {

` `for (int col = 0; col < GameMain.COLS; ++col) {

` `if (cells[row][col].content == Seed.EMPTY) {

// an empty seed found, not a draw, exit

` `return false;

` `}

` `}

` `}

` `return true; // no empty cell, it's a draw

` `}

` `/\*\* Return true if the player with "seed" has won after placing at

` `(seedRow, seedCol) \*/

` `public boolean hasWon(Seed seed, int seedRow, int seedCol) {

` `return (cells[seedRow][0].content == seed // 3-in-the-row

` `&& cells[seedRow][1].content == seed

` `&& cells[seedRow][2].content == seed

` `|| cells[0][seedCol].content == seed // 3-in-the-column

` `&& cells[1][seedCol].content == seed

`         `&& cells[2][seedCol].content == seed

` `|| seedRow == seedCol // 3-in-the-diagonal

` `&& cells[0][0].content == seed

` `&& cells[1][1].content == seed

` `&& cells[2][2].content == seed

` `|| seedRow + seedCol == 2 // 3-in-the-opposite-diagonal

` `&& cells[0][2].content == seed

` `&& cells[1][1].content == seed

` `&& cells[2][0].content == seed);

` `}

` `/\*\* Paint itself on the graphics canvas, given the Graphics context \*/

` `public void paint(Graphics g) {

` `// Draw the grid-lines

` `g.setColor(Color.GRAY);

` `for (int row = 1; row < GameMain.ROWS; ++row) {

` `g.fillRoundRect(0, GameMain.CELL\_SIZE \* row -

GameMain.GRID\_WIDHT\_HALF,

` `GameMain.CANVAS\_WIDTH-1, GameMain.GRID\_WIDTH,

` `GameMain.GRID\_WIDTH, GameMain.GRID\_WIDTH);

` `}

` `for (int col = 1; col < GameMain.COLS; ++col) {

` `g.fillRoundRect(GameMain.CELL\_SIZE \* col -

GameMain.GRID\_WIDHT\_HALF, 0,

` `GameMain.GRID\_WIDTH, GameMain.CANVAS\_HEIGHT - 1,

` `GameMain.GRID\_WIDTH, GameMain.GRID\_WIDTH);

` `}

` `// Draw all the cells

` `for (int row = 0; row < GameMain.ROWS; ++row) {

` `for (int col = 0; col < GameMain.COLS; ++col) {

` `cells[row][col].paint(g); // ask the cell to paint itself

` `}

` `}

` `}

}

` `Kelas **Board** ini berfungsi sebagai pengelola papan permainan dalam permainan Tic-Tac-Toe dan berinteraksi dengan sel-sel individu yang digunakan untuk menggambar isi sel dan menentukan hasil permainan.

- **Cell[][] cells**: Ini adalah atribut yang mewakili papan permainan sebagai matriks 2D dari objek **Cell**. Setiap sel pada papan direpresentasikan oleh objek **Cell**.
- Konstruktor **Board()**: Konstruktor ini digunakan untuk menginisialisasi papan permainan. Pada saat konstruksi, ia membuat objek **Cell** untuk setiap sel pada papan dan menyimpannya dalam matriks **cells**.
- Metode **init()**: Metode ini digunakan untuk menginisialisasi kembali papan permainan dengan menghapus isi sel-selnya sehingga papan siap digunakan untuk permainan baru.
- Metode **isDraw()**: Metode ini digunakan untuk menentukan apakah permainan berakhir dalam kondisi imbang (draw) atau tidak. Ini memeriksa setiap sel pada papan; jika ada setidaknya satu sel yang masih kosong, maka permainan tidak berakhir dengan imbang.
- Metode **hasWon(Seed seed, int seedRow, int seedCol)**: Metode ini digunakan untuk menentukan apakah pemain dengan tanda (Seed) tertentu telah memenangkan permainan setelah menempatkan tanda mereka di sel tertentu (seedRow, seedCol). Ini memeriksa apakah ada tiga tanda berurutan dalam baris, kolom, diagonal, atau diagonal berlawanan dari sel yang dipilih.
- Metode **paint(Graphics g)**: Metode ini digunakan untuk menggambar papan permainan dan sel-selnya pada kanvas grafis. Ini menggambar garis-garis pembatas antar sel (grid) dan meminta setiap sel untuk menggambar tanda mereka sendiri menggunakan metode **paint()** yang ada dalam kelas **Cell**.













package TicTacToe;

import java.awt.\*;

import java.awt.event.\*;

import javax.swing.\*;

/\*\*

\* Tic-Tac-Toe: Two-player Graphic version with better OO design.

\* The Board and Cell classes are separated in their own classes.

\*/

@SuppressWarnings("serial")

public class GameMain extends JPanel {

` `// Named-constants for the game board

` `public static final int ROWS = 3; // ROWS by COLS cells

` `public static final int COLS = 3;

` `public static final String TITLE = "Tic Tac Toe";

` `// Name-constants for the various dimensions used for graphics drawing

` `public static final int CELL\_SIZE = 100; // cell width and height (square)

` `public static final int CANVAS\_WIDTH = CELL\_SIZE \* COLS; // the drawingcanvas

` `public static final int CANVAS\_HEIGHT = CELL\_SIZE \* ROWS;

` `public static final int GRID\_WIDTH = 8; // Grid-line's width

` `public static final int GRID\_WIDHT\_HALF = GRID\_WIDTH / 2; // Grid-line'shalf-width

` `// Symbols (cross/nought) are displayed inside a cell, with padding from border

` `public static final int CELL\_PADDING = CELL\_SIZE / 6;

` `public static final int SYMBOL\_SIZE = CELL\_SIZE - CELL\_PADDING \* 2;

` `public static final int SYMBOL\_STROKE\_WIDTH = 8; // pen's stroke width

` `private Board board; // the game board

` `private GameState currentState;//the current state of the game

` `private Seed currentPlayer; // the current player

` `private JLabel statusBar; // for displaying status message

` `/\*\* Constructor to setup the UI and game components \*/

` `public GameMain() {

` `// This JPanel fires MouseEvent

` `this.addMouseListener(new MouseAdapter() {

` `@Override

` `public void mouseClicked(MouseEvent e) { // mouse-clicked handler

` `int mouseX = e.getX();

` `int mouseY = e.getY();

` `// Get the row and column clicked

` `int rowSelected = mouseY / CELL\_SIZE;

` `int colSelected = mouseX / CELL\_SIZE;

` `if (currentState == GameState.PLAYING) {

` `if (rowSelected >= 0 && rowSelected < ROWS

` `&& colSelected >= 0 && colSelected < COLS

&& board.cells[rowSelected][colSelected].content ==

Seed.EMPTY) {

` `board.cells[rowSelected][colSelected].content =

currentPlayer; // move

` `updateGame(currentPlayer, rowSelected, colSelected); //update currentState

` `// Switch player

currentPlayer = (currentPlayer == Seed.CROSS) ?

Seed.NOUGHT : Seed.CROSS;

` `}

` `} else { // game over

` `initGame(); // restart the game

` `}

` `// Refresh the drawing canvas

` `repaint(); // Call-back paintComponent().

` `}

` `});

` `// Setup the status bar (JLabel) to display status message

` `statusBar = new JLabel(" ");

` `statusBar.setFont(new Font(Font.DIALOG\_INPUT, Font.BOLD, 14));

` `statusBar.setBorder(BorderFactory.createEmptyBorder(2, 5, 4, 5));

` `statusBar.setOpaque(true);

` `statusBar.setBackground(Color.LIGHT\_GRAY);

` `setLayout(new BorderLayout());

` `add(statusBar, BorderLayout.PAGE\_END); // same as SOUTH

` `setPreferredSize(new Dimension(CANVAS\_WIDTH, CANVAS\_HEIGHT + 30));

` `// account for statusBar in height

` `board = new Board(); // allocate the game-board

` `initGame(); // Initialize the game variables

` `}

` `/\*\* Initialize the game-board contents and the current-state \*/

` `public void initGame() {

` `for (int row = 0; row < ROWS; ++row) {

` `for (int col = 0; col < COLS; ++col) {

` `board.cells[row][col].content = Seed.EMPTY; // all cells empty

` `}

` `}

` `currentState = GameState.PLAYING; // ready to play

` `currentPlayer = Seed.CROSS; // cross plays first

` `}

` `/\*\* Update the currentState after the player with "theSeed" has placed on (row, col) \*/

` `public void updateGame(Seed theSeed, int row, int col) {

` `if (board.hasWon(theSeed, row, col)) { // check for win

` `currentState = (theSeed == Seed.CROSS) ? GameState.CROSS\_WON :

GameState.NOUGHT\_WON;

` `} else if (board.isDraw()) { // check for draw

` `currentState = GameState.DRAW;

` `}

` `// Otherwise, no change to current state (PLAYING).

` `}

` `/\*\* Custom painting codes on this JPanel \*/

` `@Override

` `public void paintComponent(Graphics g){

` `//invoke via repaint()

` `super.paintComponent(g); // fill background

` `setBackground(Color.WHITE); // set its background color

` `board.paint(g); // ask the game board to paint itself

` `// Print status-bar message

` `if (currentState == GameState.PLAYING) {

` `statusBar.setForeground(Color.BLACK);

` `if (currentPlayer == Seed.CROSS) {

` `statusBar.setText("X's Turn");

` `} else {

` `statusBar.setText("O's Turn");

` `}

` `} else if (currentState == GameState.DRAW) {

` `statusBar.setForeground(Color.RED);

` `statusBar.setText("It's a Draw! Click to play again.");

` `} else if (currentState == GameState.CROSS\_WON) {

` `statusBar.setForeground(Color.RED);

` `statusBar.setText("'X' Won! Click to play again.");

` `} else if (currentState == GameState.NOUGHT\_WON) {

` `statusBar.setForeground(Color.RED);

` `statusBar.setText("'O' Won! Click to play again.");

` `}

` `}

` `/\*\* The entry "main" method \*/

` `public static void main(String[] args) {

` `// Run GUI construction codes in Event-Dispatching thread for thread safety

` `javax.swing.SwingUtilities.invokeLater(new Runnable() {

`     `public void run() {

` `JFrame frame = new JFrame(TITLE);

` `// Set the content-pane of the JFrame to an instance of main JPanel

` `frame.setContentPane(new GameMain());

` `frame.setDefaultCloseOperation(JFrame.EXIT\_ON\_CLOSE);

` `frame.pack();

` `// center the application window

` `frame.setLocationRelativeTo(null);

` `frame.setVisible(true); // show it

` `}

` `});

` `}

}

Kelas **GameMain** berfungsi sebagai pengendali utama permainan Tic-Tac-Toe dan mengintegrasikan antara logika permainan, GUI, dan respons terhadap tindakan pengguna. Ini adalah bagian sentral dari implementasi permainan dalam bentuk aplikasi grafis.

- **Named-constants**: Ini adalah konstanta yang digunakan untuk menentukan ukuran papan permainan, ukuran sel, judul permainan, lebar garis grid, ukuran simbol (X atau O), dan lain-lain. Ini digunakan untuk mengatur parameter penting dalam permainan.
- **Atribut dan Objek**:
  - **Board board**: Ini adalah objek yang merepresentasikan papan permainan. Kelas **Board** digunakan untuk mengelola sel-sel di papan.
  - **GameState currentState**: Ini adalah enumerasi yang merepresentasikan status permainan saat ini (PLAYING, DRAW, CROSS\_WON, atau NOUGHT\_WON).
  - **Seed currentPlayer**: Ini adalah enumerasi yang merepresentasikan pemain yang sedang melakukan giliran saat ini (CROSS atau NOUGHT).
  - **JLabel statusBar**: Ini adalah komponen label yang digunakan untuk menampilkan pesan status permainan kepada pengguna.
- **Konstruktor GameMain()**: Konstruktor ini digunakan untuk menginisialisasi antarmuka pengguna, termasuk menyiapkan kanvas permainan, status bar, dan inisialisasi game dengan memanggil **initGame()**.
- **Metode initGame()**: Metode ini digunakan untuk menginisialisasi papan permainan dan status permainan untuk memulai permainan baru. Ini mengosongkan semua sel di papan dan mengatur pemain pertama sebagai pemain "CROSS".
- **Metode updateGame(Seed theSeed, int row, int col)**: Metode ini digunakan untuk memperbarui status permainan setelah pemain dengan tanda tertentu menempatkan tanda mereka di sel tertentu. Ini memeriksa apakah pemain tersebut telah memenangkan permainan atau jika permainan berakhir dengan hasil imbang.
- **Metode paintComponent(Graphics g)**: Metode ini digunakan untuk menggambar elemen-elemen permainan di kanvas grafis. Ini termasuk menggambar papan permainan, sel-sel, garis pembatas, dan status bar. Pesan status juga ditampilkan berdasarkan status permainan saat ini.
- **Metode main(String[] args)**: Metode ini adalah titik masuk utama untuk menjalankan aplikasi permainan. Ini menciptakan objek **GameMain**, menyiapkan GUI, dan menampilkan permainan kepada pengguna dalam jendela.













import javax.swing.\*;

/\*\* Tic-tac-toe Applet \*/

@SuppressWarnings("serial")

public class AppletMain extends JApplet {

/\*\* init() to setup the GUI components \*/

@Override

public void init() {

// Run GUI codes in the Event-Dispatching thread for thread safety

try {

// Use invokeAndWait() to ensure that init() exits after GUI construction

SwingUtilities.invokeAndWait(new Runnable() {

@Override

public void run() {

` `setContentPane(new GameMain());

` `}

});

} catch (Exception e) {

e.printStackTrace();

}

}

}

Applet ini memungkinkan permainan Tic-Tac-Toe untuk dijalankan di dalam elemen **<applet>** pada halaman web atau dalam kontainer yang mendukung applet Java. AppletMain akan menginisialisasi dan menampilkan permainan Tic-Tac-Toe ke pengguna ketika applet dijalankan dalam lingkungan yang sesuai.

- **AppletMain** adalah subkelas dari **JApplet**, yang merupakan bagian dari API Java Swing untuk membuat applet.
- Metode **init()** adalah metode yang diwajibkan untuk applet. Ini digunakan untuk menyiapkan komponen GUI dan menjalankan kode GUI dalam utas Event-Dispatching untuk keamanan thread.

Pada intinya, **init()** melakukan hal berikut:

- Menggunakan **SwingUtilities.invokeAndWait(new Runnable())** untuk memastikan bahwa inisialisasi GUI dilakukan dalam utas Event-Dispatching.
- Setelah inisialisasi GUI selesai, applet menambahkan **GameMain** (kelas utama permainan) ke kontennya dengan menggunakan **setContentPane(new GameMain())**. Dengan demikian, permainan Tic-Tac-Toe akan dijalankan dalam applet ini ketika applet dimuat di browser atau dalam kontainer applet yang sesuai.



<html>

` `<head>

` `<title>Tic Tac Toe</title>

` `</head>

<body>

` `<h1>Tic Tac Toe</h1>

` `<applet code="AppletMain.class" width="300" height="330" alt="Error

Loading Applet?!"> Your browser does not seem to support &lt;APPLET&gt;

tag!

` `</applet>

</body>

</html>

halaman web sederhana yang mencoba untuk menampilkan applet Tic-Tac-Toe yang Anda sebutkan sebelumnya menggunakan tag **<applet>**. Ini adalah cara klasik untuk menanamkan applet Java ke dalam halaman web.

Namun, perlu diingat bahwa penggunaan applet Java semakin kurang umum karena masalah keamanan dan dukungan terbatas oleh banyak browser modern. Banyak browser modern menghentikan dukungan untuk applet Java, sehingga applet mungkin tidak akan berfungsi dengan benar atau bahkan tidak akan tampil sama sekali di beberapa browser.

Dalam hal ini, Anda mencoba untuk memuat applet dengan tag **<applet>**, yang mengacu pada file **AppletMain.class**. Applet tersebut seharusnya adalah **AppletMain** yang menginisialisasi dan menampilkan permainan Tic-Tac-Toe. Lebar dan tinggi applet ditentukan sebagai 300x330 piksel.

Pesan yang ditampilkan di dalam tag applet ("Your browser does not seem to support <APPLET> tag!") adalah pesan alternatif yang akan ditampilkan jika applet tidak dapat dimuat atau jika browser tidak mendukung tag **<applet>**.

1. Hasil Percobaan

![](Aspose.Words.6067238c-2fce-48c9-93d5-e90d7f9472b1.001.png)Ketika DRAW










![](Aspose.Words.6067238c-2fce-48c9-93d5-e90d7f9472b1.002.png)Ketika “X” menang

Ketika “O” menang

![](Aspose.Words.6067238c-2fce-48c9-93d5-e90d7f9472b1.003.png)
