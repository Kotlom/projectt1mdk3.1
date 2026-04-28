# projectt1mdk3.1
package org.example.pr2;

import java.net.URL;
import java.util.Random;
import java.util.ResourceBundle;

import javafx.event.ActionEvent;
import javafx.event.EventTarget;
import javafx.fxml.FXML;
import javafx.scene.AmbientLight;
import javafx.scene.Group;
import javafx.scene.PerspectiveCamera;
import javafx.scene.PointLight;
import javafx.scene.control.*;
import javafx.scene.input.MouseButton;
import javafx.scene.input.MouseEvent;
import javafx.scene.input.ScrollEvent;
import javafx.scene.layout.AnchorPane;
import javafx.scene.paint.Color;
import javafx.scene.paint.Paint;
import javafx.scene.paint.PhongMaterial;
import javafx.scene.shape.Box;
import javafx.scene.shape.Circle;
import javafx.scene.shape.Line;
import javafx.scene.shape.Rectangle;
import javafx.scene.transform.Rotate;
import javafx.scene.transform.Translate;

public class HelloController {

    @FXML
    private ResourceBundle resources;

    @FXML
    private URL location;

    @FXML
    private Circle circle;
    Random random = new Random();
    private Color generateRandomColor(Random random) {
    return Color.rgb(random.nextInt(256), random.nextInt(256), random.nextInt(256));
}


    @FXML
    private SplitMenuButton form;

    @FXML
    private MenuItem menucircle;

    @FXML
    private MenuItem menuline;

    @FXML
    private MenuItem menurectangle;

    @FXML
    private Tab pane1;

    @FXML
    private Tab pane2;

    @FXML
    private Tab tabpane3;
    @FXML
    private TabPane TabPane;
    @FXML
    private Box Box = new Box(200, 200, 200);
    private Rotate rotateXAxis;
    private Rotate rotateYAxis;
    private Translate translate;
    private PhongMaterial material = new PhongMaterial();

    private final double mouseSensitivity = 0.1;
    private final double movementSpeed = 10.0;
    private double mouseOldX, mouseOldY;
    private double mouseDeltaX, MouseDeltaY;

    @FXML
    private AnchorPane Pane;
    @FXML
    private AnchorPane pane3 = new AnchorPane();
    private PerspectiveCamera camera;
    private final double rotationSpeed = 45.0;
    Group modelGroup = new Group();
    @FXML
    private Rectangle rectangle;
    @FXML
    private Slider slider;

    Line line2;
    Circle circle2;
    Rectangle rectangle2;
    double startMouseX;
    double StartMouseY;
    double endMouseX;
    double EndMouseY;
    @FXML
    private SplitMenuButton color;


    private Color color4;

    @FXML
    private MenuItem color2;

    @FXML
    private MenuItem color3;

    @FXML
    void ScrollPane3(ScrollEvent event) {
double delta = event.getDeltaY();
if (delta > 0) {
    translate.setZ(translate.getZ() + movementSpeed);
} else {
    translate.setZ(translate.getZ() - movementSpeed);

}
        System.out.println("scroll");
    }

    @FXML
    void actionPressedPane3(MouseEvent event) {
if (event.getButton() == MouseButton.PRIMARY) {
    mouseDeltaX = event.getSceneX();
    MouseDeltaY = event.getSceneY();
    System.out.println("press");
}
    }

    @FXML
    void pane3Dragged(MouseEvent event) {
        if (event.isPrimaryButtonDown()) {
            mouseDeltaX = event.getSceneX() - mouseOldX;
            MouseDeltaY = event.getSceneY() - mouseOldY;
            rotateXAxis.setAngle(rotateXAxis.getAngle() - MouseDeltaY * mouseSensitivity);
            rotateYAxis.setAngle(rotateYAxis.getAngle() + mouseDeltaX * mouseSensitivity);
            mouseOldX = event.getSceneX();
            mouseOldY = event.getSceneY();
            System.out.println("dragged");
        }
    }
public void Box(){
    translate= new Translate();
    material.setDiffuseColor(Color.OLIVE);
    Box.setMaterial(material);
    rotateXAxis = new Rotate(0, Rotate.X_AXIS);
    rotateYAxis = new Rotate(0, Rotate.Y_AXIS);
    modelGroup.getTransforms().addAll(translate, rotateXAxis, rotateYAxis);
    modelGroup.getChildren().add(Box);
            AmbientLight ambientLight = new AmbientLight(Color.WHITE);
            PointLight pointLight = new PointLight(Color.WHITE);
            pointLight.setTranslateX(800);
            pointLight.setTranslateY(-700);
            pointLight.setTranslateZ(-300);
            pane3.getChildren().addAll(modelGroup, ambientLight, pointLight);
        }


    @FXML
    void OnMouseClick(MouseEvent event) {
        if (event.getButton()== MouseButton.PRIMARY){
            System.out.println(circle.getFill());
            circle.setFill(generateRandomColor(random));
        }
        else if (event.getButton()==MouseButton.SECONDARY) {
            circle.setFill(Paint.valueOf("linear-gradient(from 0.0% 0.0% to 100.0% 100.0%, 0x803f19ff 0.0%, 0xffffffff 100.0%)"));
        }
    }

    @FXML
    void OnMouseExited(MouseEvent event) {
rectangle.setFill(Paint.valueOf("linear-gradient(from 0.0% 0.0% to 100.0% 100.0%, 0x803f19ff 0.0%, 0xffffffff 100.0%)"));
    }

    @FXML
    void OnMouseMoved(MouseEvent event) {
        rectangle.setFill(generateRandomColor(random));
    }
    @FXML
    void OnMousePressed(MouseEvent event) {
        anchorX = event.getSceneX();
        anchorY = event.getSceneY();
        startAngle = line.getRotate();
    }
    @FXML
    private Line line;
    private double startAngle;
    private double anchorX, anchorY;
    @FXML
    void OnMouseDragged(MouseEvent event) {
        double deltaX = event.getSceneX() - anchorX;
        double deltaY = event.getSceneY() - anchorY;
        double newAngle = Math.atan2(deltaY, deltaX) * 100 / Math.PI + 90;
                line.setRotate(startAngle + newAngle);
    }
    @FXML
    void OnScroll(ScrollEvent event) {
        EventTarget objects = event.getTarget();
        if (objects instanceof Circle) {
            if (event.getDeltaY() > 0) {
                circle.setRadius(circle.getRadius() + 5 );
            } else if (event.getDeltaY() < 0){
                circle.setRadius(circle.getRadius() - 5);
            }
        }
        else if (objects instanceof Line) {
            if (event.getDeltaY() > 0) {
                line.setStrokeWidth(line.getStrokeWidth()*1.05);
            } else if (objects instanceof Line) {
                line.setStrokeWidth(line.getStrokeWidth()/1.05);
            }
        }
        else if(objects instanceof Rectangle) {
            if (event.getDeltaY() > 0) {
                rectangle.setWidth(rectangle.getWidth()*1.05);
                rectangle.setHeight(rectangle.getHeight()*1.05);
            } else if (event.getDeltaY() < 0) {
                rectangle.setWidth(rectangle.getWidth()/1.05);
                rectangle.setHeight(rectangle.getHeight()/1.05);
            }
        }
    }

    @FXML
    void ActionBlack(ActionEvent event) {
        color.setText("черный");
    }

    @FXML
    void ActionMenuCircle(ActionEvent event) {
form.setText("круг");
    }

    @FXML
    void ActionMenuLine(ActionEvent event) {
form.setText("линия");
    }

    @FXML
    void ActionMenuRectangle(ActionEvent event) {
        form.setText("прямоугольник");
    }

    @FXML
    void ActionRed(ActionEvent event) {
color.setText("красный");
    }
    @FXML
    void ActionBlue(ActionEvent event) {
color.setText("синий");
    }
    @FXML
    void paneclick(MouseEvent event) {

    }
    @FXML
    void panedragged(MouseEvent event) {
endMouseX=event.getX();
EndMouseY=event.getY();
switch (form.getText()){
    case "линия":
        line2.setEndX(endMouseX);
        line2.setEndY(EndMouseY);
        break;
    case "круг":
        double radius = Math.sqrt(Math.pow((startMouseX - endMouseX), 2)
                + Math.pow((StartMouseY - EndMouseY), 2));
        circle2.setRadius(radius);
        break;
    case "прямоугольник":
        rectangle2.setWidth(Math.abs(startMouseX - endMouseX));
        rectangle2.setHeight(Math.abs(StartMouseY - EndMouseY));
        rectangle2.setX(Math.min(startMouseX, endMouseX));
        rectangle2.setY(Math.min(StartMouseY, EndMouseY));
        break;
}
    }

    @FXML
    void panepresed(MouseEvent event) {
        if (color.getText().equals("красный")) {
            color4 = Color.RED;
        } else if (color.getText().equals("синий")) {
            color4 = Color.BLUE;
        } else if (color.getText().equals("черный")) {
            color4 = Color.BLACK;
        }
        startMouseX = event.getX();
        StartMouseY = event.getY();
        switch (form.getText()) {

            case "круг":
                System.out.println(form.getText());
                System.out.println("круг");
                circle2 = new Circle(startMouseX, StartMouseY, 0);
                circle2.setFill(color4);
                circle2.setStroke(Color.RED);
                circle2.setStrokeWidth(slider.getValue());
                Pane.getChildren().addAll(circle2);
                break;
            case "линия":
                System.out.println("линия");
                line2 = new Line(startMouseX, StartMouseY, event.getX() + 1, event.getY() + 1);
                line2.setStrokeWidth(slider.getValue());
                line2.setStroke(color4);
                Pane.getChildren().addAll(line2);
                break;
            case "прямоугольник":
                System.out.println("прямоугольник");
                rectangle2 = new Rectangle(startMouseX, StartMouseY, 20, 20);
                rectangle2.setFill(color4);
                rectangle2.setStroke(Color.RED);
                rectangle2.setStrokeWidth(slider.getValue());
                Pane.getChildren().addAll(rectangle2);
                break;
        }
    }

    @FXML
    void initialize() {
        assert circle != null : "fx:id=\"circle\" was not injected: check your FXML file 'hello-view.fxml'.";
        assert rectangle != null : "fx:id=\"rectangle\" was not injected: check your FXML file 'hello-view.fxml'.";
Box();
camera = new PerspectiveCamera(true);
camera.setTranslateZ(-500);
    }

}
