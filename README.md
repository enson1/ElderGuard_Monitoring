# AI-Powered Health & Security Monitoring System

## Overview

This is a comprehensive Flask-based application that combines advanced computer vision and machine learning capabilities to provide real-time health monitoring, security features, and accessibility tools. The system is designed to monitor elderly care, detect emergencies, provide sign language translation, and offer secure face recognition authentication.

## Key Features

### 🏥 **Fall Detection & Health Monitoring**
- Real-time fall detection using YOLOv8 pose estimation and MediaPipe
- Configurable sensitivity levels and detection thresholds
- Automatic video snippet capture when falls are detected
- Email and Telegram alert notifications
- Support for both live webcam monitoring and uploaded video analysis

### 👏 **Activity Tracking (Clap Detection)**
- Real-time clap counting with configurable targets
- Session tracking with calorie burn estimation
- Visual feedback and sound cues
- Database storage of activity sessions

### 🤝 **Sign Language Translation**
- Real-time American Sign Language (ASL) detection
- Custom CNN model for alphabet recognition
- Text-to-speech capability for detected signs
- Adjustable confidence thresholds and UI accessibility features

### 👤 **Face Recognition Security**
- Multi-pose face registration system
- Secure PIN-based authentication combined with facial recognition
- Real-time face detection using DNN and Dlib
- User profile management with encrypted credentials

### 📊 **Event History & Analytics**
- Comprehensive event logging for all detected incidents
- Searchable and filterable event history
- Export capabilities for data analysis
- Visual charts and statistics

### 🔔 **Multi-Channel Alerting**
- Email notifications with SMTP support
- Telegram bot integration
- In-app notifications
- Configurable alert schedules and emergency contacts

## System Architecture

```
├── app.py                    # Main Flask application with integrated features
├── detection.py              # Core pose estimation and fall detection logic
├── clap_tracker.py          # Clap detection and tracking module
├── sign_detector_logic.py   # ASL detection neural network logic
├── config.json              # Application configuration
├── requirements.txt         # Python dependencies
├── templates/               # HTML templates
│   ├── index.html          # Main dashboard
│   ├── event_history.html  # Event history viewer
│   ├── login.html          # Face recognition login
│   ├── register.html       # User registration
│   ├── face_registration.html # Face capture interface
│   ├── private_data.html   # Secure user area
│   └── sign_lang_trans.html # Sign language interface
├── uploads/                 # User uploaded videos
├── processed/              # Processed videos and snippets
├── temp_alerts/            # Temporary alert images
└── instance/               # Instance-specific data

## Machine Learning Models

The application uses several pre-trained models:

- **YOLOv8n-pose.pt**: Human pose estimation for fall detection
- **custom_cnn_sign_language_best.keras**: Custom CNN for ASL alphabet recognition
- **dlib_face_recognition_resnet_model_v1.dat**: Face recognition embeddings
- **shape_predictor_68_face_landmarks.dat**: Facial landmark detection
- **res10_300x300_ssd_iter_140000.caffemodel**: DNN face detection
- **deploy.prototxt**: Network architecture for Caffe model

## Installation

### Prerequisites

- Python 3.8 or higher
- Webcam (for real-time features)
- CUDA-capable GPU (optional, for better performance)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd <project-directory>
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   Create a `.env` file in the root directory:
   ```env
   FLASK_SECRET_KEY=your_secret_key_here
   TELEGRAM_BOT_TOKEN=your_telegram_bot_token
   TELEGRAM_CHAT_ID=your_telegram_chat_id
   ```

5. **Configure application settings**
   Edit `config.json` to set:
   - Fall detection sensitivity
   - Email SMTP settings
   - Emergency contacts
   - Alert preferences

6. **Initialize database**
   ```bash
   python app.py
   ```
   The database will be created automatically on first run.

## Usage

### Starting the Application

```bash
python app.py
```

The application will be available at `http://localhost:5000`

### Main Dashboard Features

1. **Fall Detection Monitoring**
   - Click "Start Webcam" to begin live monitoring
   - Upload videos for offline analysis
   - Configure detection sensitivity in System Settings

2. **Activity Tracking**
   - Set clap target and start tracking
   - View session history and statistics

3. **Sign Language Translation**
   - Navigate to Sign Language tab
   - Start camera and begin signing
   - View real-time translations

4. **Face Recognition Login**
   - Register new users with face capture
   - Login using face recognition + PIN

### API Endpoints

- `/start_webcam` - Start fall detection monitoring
- `/stop_webcam` - Stop monitoring
- `/upload` - Upload video for processing
- `/start_clap_tracker` - Start clap detection
- `/asl/start_camera` - Start ASL detection
- `/fr_home` - Face recognition home
- `/event_history` - View event logs

## Configuration

### Fall Detection Settings

Configure in `config.json`:
```json
{
  "fall_detection": {
    "enabled": true,
    "sensitivity": "Medium (Balanced)",
    "min_kpt_confidence": 0.3,
    "velocity_threshold": 0.4,
    "confidence_threshold": 0.7
  }
}
```

### Email Alerts

Configure SMTP settings:
```json
{
  "email_alerting": {
    "enabled": true,
    "smtp_server": "smtp.gmail.com",
    "smtp_port": 587,
    "smtp_user": "your_email@gmail.com",
    "smtp_password": "your_app_password"
  }
}
```

## Development

### Project Structure

- **Core Services**: `CameraService` and `ProcessingManager` handle resource management
- **Detection Modules**: Separate modules for fall, clap, and sign detection
- **Database Models**: SQLAlchemy models for users, events, and sessions
- **Threading**: Async processing for video streams and background tasks

### Adding New Features

1. Create new detection module in separate file
2. Integrate with `CameraService` for camera access
3. Add routes to `app.py`
4. Update dashboard UI in `templates/index.html`

## Troubleshooting

### Common Issues

1. **Camera not working**
   - Check camera permissions
   - Ensure no other application is using the camera
   - Verify camera index in configuration

2. **Model loading errors**
   - Ensure all model files are in the project root
   - Check file permissions
   - Verify model compatibility with installed libraries

3. **Email alerts not sending**
   - Use app-specific passwords for Gmail
   - Check firewall settings
   - Verify SMTP configuration

## Thing to take note 
  - ASL dataset can be download at 'https://www.kaggle.com/datasets/debashishsau/aslamerican-sign-language-aplhabet-dataset/data'
  - shape_predictor_68_face_landmarks.dat can be download at the google drive



## Acknowledgments

- YOLOv8 by Ultralytics
- Dlib face recognition
- MediaPipe by Google
- Flask community

