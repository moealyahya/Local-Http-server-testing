import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;
import java.io.IOException;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class HTTPServer {
    public static void main(String args[]) throws IOException {
        final ServerSocket server = new ServerSocket(8080); // server opens and creates a connection
        System.out.println("Server started on  port 8080..."); //just to show that the connection is open

        while (true) {
            final Socket client = server.accept(); //client is now created and connects to the server
            System.out.println("Client connected to server...");

            InputStreamReader reader = new InputStreamReader(client.getInputStream()); //what will read the raw content in the server
            BufferedReader decoder = new BufferedReader(reader); //decodes raw content

            //reading from http
            String line = decoder.readLine();
            while (!line.isEmpty()) {
                System.out.println(line);
                line = decoder.readLine();
            }

            // some functionality to process and prepare data to send back to client
            LocalDateTime currentDate = LocalDateTime.now(); //getting date and time from website
            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
            String formattedDateTime = currentDate.format(formatter);

            //http response creation format
            String title = "Local Experimental HTTP Server";
            String htmlResponse = "<html>" +
                    "<head><title>" + title + "</title></head>" +
                    "<body style='font-family: Arial; text-align: center; margin-top: 50px;'>" +
                    "<h1>" + title + "</h1>" +
                    "<p>Current date and time: <b>" + formattedDateTime + "</b></p>" +
                    "</body></html>";

            //http header creation format
            String httpResponse =
                    "HTTP/1.1 200 OK\r\n" +
                            "Content-Type: text/html; charset=UTF-8\r\n" +
                            "Content-Length: " + htmlResponse.getBytes().length + "\r\n" +
                            "Connection: close\r\n" +
                            "\r\n" +
                            htmlResponse;

            //Send the response back to the client
            OutputStream outputStream = client.getOutputStream();
            outputStream.write(httpResponse.getBytes());
            outputStream.flush();

            client.close();
        }
    }
}

// To use: compile and run this Java program (it acts as a web server). Then open a browser and go to http://localhost:8080/ to connect to it.
// This Java program is the server: it waits for clients, reads their requests, and responds with HTML.
// The browser (localhost:8080) is the client: it sends an HTTP request (like GET /) and displays the response it receives.
