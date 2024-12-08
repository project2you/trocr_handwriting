
# Thai Handwriting OCR Model

A comprehensive pipeline for Optical Character Recognition (OCR) of Thai handwriting using **Vision Transformer (ViT)** and **RoBERTa** for decoding text.

---

## **Model Architecture**

```
Input Image --> ContourExtractor --> Vision Encoder --> Text Decoder --> Output Text
```

#### **Component Descriptions**
1. **ContourExtractor**: Extracts character contours from the input image.
2. **Vision Encoder (ViT)**: Converts the contour image into a feature representation using self-attention.
3. **Text Decoder (RoBERTa)**: Transforms features into readable text.

---

## **Dataset Pipeline**

1. **Dataset**: [Thai Handwriting Dataset](#) (Link to dataset if applicable).
2. **Splitting**: 
   - **Training Set**: 80%
   - **Validation Set**: 10%
   - **Test Set**: 10%
3. **Preprocessing**:
   - Resize all images to **384x384**.
   - Apply **Data Augmentation** for training (rotation, scaling, noise, etc.).
   - Generate **Contour Mask**.
   - Convert images to tensors.

---

## **Training Pipeline**

### **1. Training Phase**
- Perform forward pass through the model.
- Calculate **Loss**:
  - **Cross Entropy Loss** for text decoding.
  - **Contour Loss** for contour extraction.
- Perform backward pass to update weights.
- Handle Out-of-Memory (OOM) issues by batch splitting if needed.

### **2. Validation Phase**
- Evaluate the model on the validation set.
- Compute metrics such as accuracy and BLEU score.
- Save the **best model** if performance improves.

### **3. Monitoring**
- Track **Loss** and **Accuracy** during training.
- Record **time and memory usage**.
- Save checkpoints and metrics.

---

## **Evaluation Metrics**

The following metrics are used for evaluation:
1. **Character-level Accuracy**: Accuracy at the character level.
2. **Word-level Accuracy**: Accuracy at the word level.
3. **BLEU Score**: Measures similarity between predicted and actual text.
4. **Text Similarity**: Evaluates textual similarity.
5. **ROC-AUC & PR-AUC**: For character-level classification.
6. **Confusion Matrix**: Shows errors for each character.

---

## **New Additions**

### **Performance Monitoring Components**
1. **PerformanceMonitor class**: Provides a unified way to track real-time performance during training and evaluation.
2. **Real-time metrics tracking**: Continuously monitors key metrics like loss, accuracy, and speed.
3. **Resource utilization monitoring**: Tracks GPU/CPU usage, memory consumption, and processing times to ensure efficient resource management.

### **Enhanced Error Handling**
1. **Automatic recovery system**: Recovers training sessions automatically after interruptions or errors.
2. **Error state logging**: Captures the exact state of the model and data when errors occur for easier debugging.
3. **Detailed error logging**: Provides comprehensive logs of exceptions, stack traces, and resource states.

### **Advanced Metrics**
1. **BLEU Score**: Evaluates how closely the predicted text matches the ground truth using a standard NLP metric.
2. **ROC/PR Curves**: Visualizes the trade-offs between precision, recall, and classification thresholds.
3. **Character-level confusion matrix**: Highlights misclassified characters for detailed error analysis.

### **Memory Optimization**
1. **Dynamic OOM handling**: Automatically adjusts batch sizes to prevent Out-of-Memory errors during training.
2. **Automatic batch size adjustment**: Dynamically tunes the batch size based on available memory.
3. **Improved cache management**: Reduces redundant data storage and optimizes memory allocation.

---

## **File Structure**

```plaintext
project/
├── checkpoints/          # Model checkpoints
├── evaluation_results/   # Plots and evaluation metrics
├── visualizations/       # Training visualizations
├── training_metrics.json # Metrics in JSON format
└── ocr_training.log      # Training logs
```

---

# โมเดล OCR สำหรับลายมือภาษาไทย

ระบบการรู้จำตัวอักษร (OCR) สำหรับลายมือภาษาไทย โดยใช้ **Vision Transformer (ViT)** และ **RoBERTa** ในการถอดรหัสข้อความ

---

## **โครงสร้างของโมเดล**

```
Input Image --> ContourExtractor --> Vision Encoder --> Text Decoder --> Output Text
```

#### **คำอธิบายของส่วนประกอบ**
1. **ContourExtractor**: สกัดเส้นขอบของตัวอักษรจากภาพอินพุต
2. **Vision Encoder (ViT)**: แปลงภาพเส้นขอบให้เป็นข้อมูลเชิงลักษณะ
3. **Text Decoder (RoBERTa)**: แปลงข้อมูลลักษณะเป็นข้อความ

---

## **การเตรียมชุดข้อมูล**

1. **ชุดข้อมูล**: [Thai Handwriting Dataset](#)
2. **การแบ่งชุดข้อมูล**:
   - **ชุดฝึกอบรม**: 80%
   - **ชุดตรวจสอบ**: 10%
   - **ชุดทดสอบ**: 10%
3. **การประมวลผลข้อมูล**:
   - ปรับขนาดภาพเป็น **384x384**
   - ใช้ **Data Augmentation** สำหรับชุดฝึกอบรม (หมุน, ย่อขยาย, noise ฯลฯ)
   - สร้าง **Contour Mask**
   - แปลงข้อมูลเป็น tensors

---

## **ขั้นตอนการฝึกโมเดล**

### **1. การฝึกโมเดล**
- ส่งข้อมูลไปข้างหน้า (forward pass)
- คำนวณ **Loss**:
  - **Cross Entropy Loss** สำหรับการถอดรหัสข้อความ
  - **Contour Loss** สำหรับการสกัดเส้นขอบ
- ส่งข้อมูลย้อนกลับ (backward pass) เพื่อปรับปรุงน้ำหนัก
- จัดการปัญหาหน่วยความจำ (OOM) โดยการแบ่ง batch หากจำเป็น

### **2. การตรวจสอบ**
- ประเมินโมเดลบนชุดตรวจสอบ
- คำนวณตัวชี้วัด เช่น ความแม่นยำ และ BLEU score
- บันทึก **โมเดลที่ดีที่สุด** หากผลการทำงานดีขึ้น

### **3. การติดตาม**
- ติดตาม **Loss** และ **Accuracy**
- บันทึก **เวลาและการใช้งานหน่วยความจำ**
- บันทึกค่า checkpoint และ metrics

---

## **สิ่งที่เพิ่มเข้ามาใหม่**

### **ส่วนประกอบสำหรับการติดตามประสิทธิภาพ**
1. **คลาส PerformanceMonitor**: ใช้ติดตามประสิทธิภาพแบบเรียลไทม์ระหว่างการฝึกและการประเมินผล
2. **การติดตาม metrics แบบเรียลไทม์**: วัดค่าต่าง ๆ เช่น Loss, Accuracy, และความเร็วในการประมวลผล
3. **การติดตามการใช้งานทรัพยากร**: ตรวจสอบการใช้งาน GPU/CPU, การใช้หน่วยความจำ, และเวลาที่ใช้ในการประมวลผล

### **การจัดการข้อผิดพลาดขั้นสูง**
1. **ระบบกู้คืนอัตโนมัติ**: เรียกคืนการฝึกได้อัตโนมัติเมื่อเกิดการขัดจังหวะหรือข้อผิดพลาด
2. **การบันทึกสถานะข้อผิดพลาด**: เก็บสถานะของโมเดลและข้อมูลเมื่อเกิดข้อผิดพลาดเพื่อการดีบักที่ง่ายขึ้น
3. **การบันทึกข้อผิดพลาดอย่างละเอียด**: ให้รายละเอียดข้อผิดพลาด เช่น ข้อยกเว้น, stack trace, และสถานะการใช้งานทรัพยากร

### **ตัวชี้วัดขั้นสูง**
1. **BLEU Score**: วัดความใกล้เคียงของข้อความพยากรณ์กับข้อความจริงด้วยค่ามาตรฐาน NLP
2. **ROC/PR Curves**: แสดงผลการแลกเปลี่ยนระหว่าง Precision และ Recall ที่ระดับต่าง ๆ
3. **Character-level Confusion Matrix**: แสดงข้อผิดพลาดในระดับตัวอักษรอย่างละเอียด

### **การปรับปรุงหน่วยความจำ**
1. **การจัดการ OOM แบบไดนามิก**: ปรับขนาด batch โดยอัตโนมัติเพื่อป้องกันข้อผิดพลาด OOM ระหว่างการฝึก
2. **การปรับขนาด batch อัตโนมัติ**: ปรับแต่ง batch size ให้เหมาะสมกับหน่วยความจำที่มี
3. **การจัดการ cache ที่ปรับปรุงแล้ว**: ลดการเก็บข้อมูลซ้ำซ้อนและปรับปรุงการจัดสรรหน่วยความจำ
