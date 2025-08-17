📌 Image Captioning with ViT + GPT-2
1. Bài toán

Sinh chú thích ảnh (Image Captioning): cho một ảnh đầu vào, mô hình sinh ra một câu mô tả bằng tiếng Anh.

Encoder: Vision Transformer (ViT) để trích xuất đặc trưng hình ảnh.

Decoder: GPT-2 để sinh câu mô tả tự nhiên, mạch lạc.

Kiến trúc: Encoder–Decoder dựa trên VisionEncoderDecoderModel của Hugging Face.

Dữ liệu huấn luyện: Flickr8k (mỗi ảnh có 1–5 caption tiếng Anh).

2. Dữ liệu & Tiền xử lý

Ảnh: resize về (224,224), chuyển tensor, chuẩn hóa (mean=0.5, std=0.5), trích đặc trưng bằng ViTFeatureExtractor.

Chú thích: tokenize bằng GPT-2 tokenizer, pad đến max_length=50, bỏ qua token pad trong loss.

Chia dữ liệu: Train 80% – Val 20%.

3. Huấn luyện

Mô hình: VisionEncoderDecoderModel.from_encoder_decoder_pretrained()

Tham số sinh caption:

max_length=128, num_beams=4, no_repeat_ngram_size=3, length_penalty=2.0.

Cấu hình huấn luyện (Seq2SeqTrainer):

Epochs: 3

Batch size: 8

Learning rate: 5e-5

Warmup steps: 1024

Evaluation: theo từng epoch

Lưu duy nhất mô hình tốt nhất (save_total_limit=1).

4. Kết quả

Similarity score: ~0.38

Mô hình sinh caption có ý nghĩa gần giống so với ground-truth, ngữ pháp tự nhiên.

5. Lý do chọn ViT + GPT-2

ViT: trích xuất quan hệ không gian toàn cục tốt hơn CNN.

GPT-2: sinh ngôn ngữ mượt mà, có ngữ nghĩa tốt.

Hugging Face: dễ triển khai, tái sử dụng và tinh chỉnh.
