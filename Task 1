import android.app.Activity;
import android.content.Context;
import android.hardware.Camera;
import android.hardware.Camera.Parameters;
import android.os.Bundle;
import android.view.View;
import android.widget.ImageButton;

public class FlashlightActivity extends Activity {
    private Camera camera;
    private boolean isFlashOn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_flashlight);

        final ImageButton toggleButton = findViewById(R.id.toggleButton);

        // Check if the device has a camera flash
        Context context = this;
        if (!context.getPackageManager().hasSystemFeature(
                android.content.pm.PackageManager.FEATURE_CAMERA_FLASH)) {
            // Handle the case where the device doesn't have a flash
            // You can show a message or disable the flashlight functionality
            return;
        }

        camera = Camera.open();
        final Parameters params = camera.getParameters();

        toggleButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (isFlashOn) {
                    // Turn off the flashlight
                    params.setFlashMode(Parameters.FLASH_MODE_OFF);
                    camera.setParameters(params);
                    camera.stopPreview();
                    isFlashOn = false;
                } else {
                    // Turn on the flashlight
                    params.setFlashMode(Parameters.FLASH_MODE_TORCH);
                    camera.setParameters(params);
                    camera.startPreview();
                    isFlashOn = true;
                }
            }
        });
    }

    @Override
    protected void onPause() {
        super.onPause();
        // Release the camera when the app is paused
        releaseCamera();
    }

    @Override
    protected void onResume() {
        super.onResume();
        // Reinitialize the camera when the app is resumed
        if (camera == null) {
            camera = Camera.open();
        }
    }

    private void releaseCamera() {
        if (camera != null) {
            camera.release();
            camera = null;
        }
    }
}
