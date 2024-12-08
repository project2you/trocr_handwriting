
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

## **ตัวชี้วัด**

ตัวชี้วัดที่ใช้ประเมินผล:
1. **ความแม่นยำในระดับตัวอักษร**: ความถูกต้องในระดับตัวอักษร
2. **ความแม่นยำในระดับคำ**: ความถูกต้องในระดับคำ
3. **BLEU Score**: ความใกล้เคียงระหว่างข้อความที่ทำนายและข้อความจริง
4. **Text Similarity**: ความคล้ายคลึงของข้อความ
5. **ROC-AUC และ PR-AUC**: สำหรับการจำแนกตัวอักษร
6. **Confusion Matrix**: แสดงข้อผิดพลาดสำหรับแต่ละตัวอักษร

---

## **โครงสร้างไฟล์**

```plaintext
project/
├── checkpoints/          # Checkpoints ของโมเดล
├── evaluation_results/   # แผนภาพและตัวชี้วัด
├── visualizations/       # การแสดงผลการฝึก
├── training_metrics.json # ตัวชี้วัดในรูปแบบ JSON
└── ocr_training.log      # ไฟล์บันทึกการฝึกโมเดล
```
