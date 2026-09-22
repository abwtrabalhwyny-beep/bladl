# bladl<?php
require_once 'db.php';

// جلب الشهادة الأولى كمثال
$stmt = $pdo->query('SELECT * FROM health_certificates LIMIT 1');
$certificate = $stmt->fetch();
?>
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منصة بلدي - شهادة صحية</title>
    <!-- استدعاء مكتبة البوتستراب للتصميم المتجاوب -->
    <link href="https://jsdelivr.net" rel="stylesheet">
    <style>
        body { background-color: #f8f9fa; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        .balady-header { background-color: #ffffff; border-bottom: 2px solid #28a745; padding: 15px 0; }
        .gov-tag { background-color: #1e4620; color: white; font-size: 12px; padding: 4px 10px; border-radius: 4px; }
        .cert-card { max-width: 500px; margin: 30px auto; background: white; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); padding: 20px; }
        .worker-img { width: 180px; height: 220px; object-fit: cover; border: 1px solid #ddd; margin: 15px auto; display: block; }
        .form-label-custom { font-weight: bold; color: #333; margin-top: 10px; font-size: 14px; }
        .form-control-custom { background-color: #f1f3f5; border: 1px solid #ced4da; padding: 10px; border-radius: 6px; color: #495057; }
    </style>
</head>
<body>

<!-- شريط الملاحة العلوي لمحاكاة التطبيق -->
<div class="balady-header shadow-sm">
    <div class="container d-flex justify-content-between align-items-center">
        <div>
            <span class="gov-tag">موقع حكومي مسجل لدى هيئة الحكومة الرقمية</span>
        </div>
        <div class="text-end">
            <small class="text-muted">خدمات بلدي | balady services</small>
        </div>
    </div>
</div>

<div class="container">
    <div class="cert-card">
        <h3 class="text-center mb-4 text-success font-weight-bold" style="border-bottom: 2px solid #eee; padding-bottom: 10px;">شهادة صحية</h3>
        
        <?php if ($certificate): ?>
            <!-- عرض صورة العامل -->
            <img src="<?php echo htmlspecialchars($certificate['worker_image']); ?>" alt="صورة العامل" class="worker-img img-thumbnail">

            <!-- حقل الأمانة -->
            <div class="mb-3">
                <label class="form-label-custom d-block text-end">الأمانة</label>
                <div class="form-control-custom text-end"><?php echo htmlspecialchars($certificate['amana']); ?></div>
            </div>

            <!-- حقل البلدية -->
            <div class="mb-3">
                <label class="form-label-custom d-block text-end">البلدية</label>
                <div class="form-control-custom text-end"><?php echo htmlspecialchars($certificate['municipality']); ?></div>
            </div>

            <!-- حقل الاسم -->
            <div class="mb-3">
                <label class="form-label-custom d-block text-end">الإسم</label>
                <div class="form-control-custom text-end" style="direction: ltr;"><?php echo htmlspecialchars($certificate['worker_name']); ?></div>
            </div>

            <!-- حقل رقم الهوية -->
            <div class="mb-3">
                <label class="form-label-custom d-block text-end">رقم الهوية</label>
                <div class="form-control-custom text-end"></div>
            </div>
        <?php else: ?>
            <div class="alert alert-danger text-center">لم يتم العثور على بيانات الشهادة الصحية.</div>
        <?php endif; ?>
    </div>
</div>

<script src="https://jsdelivr.net"></script>
</body>
</html>
