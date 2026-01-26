# 📸 Photo Album App - Software Requirements Specification

> **Project**: Photo Album Application for Android  
> **Version**: 1.0  
> **Last Updated**: January 26, 2026  
> **Platform**: Android (API 30+)  
> **Languages**: Java, XML  
> **Design**: Apple-style UI/UX

---

## 📋 Mục lục

1. [Tổng quan dự án](#1-tổng-quan-dự-án)
2. [Phân hệ người dùng](#2-phân-hệ-người-dùng)
3. [Module Quản lý ảnh](#3-module-quản-lý-ảnh)
4. [Module Xem ảnh](#4-module-xem-ảnh)
5. [Module Chỉnh sửa ảnh](#5-module-chỉnh-sửa-ảnh)
6. [Module Album](#6-module-album)
7. [Module Yêu thích](#7-module-yêu-thích)
8. [Module Thùng rác](#8-module-thùng-rác)
9. [Module Ảnh ẩn](#9-module-ảnh-ẩn)
10. [Module Slideshow](#10-module-slideshow)
11. [Module Tải ảnh từ URL](#11-module-tải-ảnh-từ-url)
12. [Module Giao diện](#12-module-giao-diện)
13. [Module Chia sẻ](#13-module-chia-sẻ)
14. [Module AI Features](#14-module-ai-features)
15. [Cơ sở dữ liệu](#15-cơ-sở-dữ-liệu)
16. [Cấu trúc dự án](#16-cấu-trúc-dự-án)
17. [Yêu cầu kỹ thuật](#17-yêu-cầu-kỹ-thuật)

---

## 1. Tổng quan dự án

### 1.1 Mô tả
Ứng dụng Album Ảnh cho Android với giao diện hiện đại theo phong cách Apple Photos, hỗ trợ đầy đủ các tính năng quản lý, chỉnh sửa ảnh và tích hợp AI.

### 1.2 Mục tiêu
- Quản lý ảnh hiệu quả với nhiều chế độ xem
- Chỉnh sửa ảnh với các filter và công cụ vẽ
- Tổ chức ảnh theo album
- Bảo vệ ảnh riêng tư
- Tích hợp AI để nâng cao trải nghiệm

### 1.3 Công nghệ sử dụng

| Thành phần | Công nghệ |
|------------|-----------|
| Language | Java |
| UI | XML, Material Design 3 |
| Database | Room Database (SQLite) |
| Image Loading | Glide |
| AI/ML | ML Kit (Google), TensorFlow Lite |
| Architecture | MVVM |
| DI | Hilt (optional) |

---

## 2. Phân hệ người dùng

### 2.1 Người dùng chính (Primary User)
Người dùng sử dụng ứng dụng trên thiết bị cá nhân, có toàn quyền truy cập các tính năng.

### 2.2 Luồng khởi động ứng dụng

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Splash     │ ──► │  Check       │ ──► │  Main       │
│  Screen     │     │  Permissions │     │  Activity   │
└─────────────┘     └──────────────┘     └─────────────┘
                           │
                           ▼ (Từ chối)
                    ┌──────────────┐
                    │  Permission  │
                    │  Rationale   │
                    └──────────────┘
```

### 2.3 Bottom Navigation Structure

```
┌─────────────────────────────────────────────────────────┐
│                      Main Content                        │
├─────────┬─────────┬─────────┬─────────┬─────────────────┤
│  📷     │  📁     │  ⭐     │  🤖     │  ⚙️            │
│ Photos  │ Albums  │ Favorite│   AI    │  Settings      │
└─────────┴─────────┴─────────┴─────────┴─────────────────┘
```

---

## 3. Module Quản lý ảnh

### 3.1 Màn hình chính - Photos

#### 3.1.1 Header
- **Large Title**: "Photos" (34sp, bold)
- **Subtitle**: Hiển thị số lượng ảnh (VD: "1,234 Photos")

#### 3.1.2 Controls Bar
| Thành phần | Mô tả |
|------------|-------|
| View Toggle | Segmented Control: Grid / List |
| Sort Button | Dropdown menu chọn kiểu sắp xếp |

#### 3.1.3 Tùy chọn sắp xếp

| Tiêu chí | Tăng dần | Giảm dần |
|----------|----------|----------|
| Ngày | Oldest First | Newest First ✓ (default) |
| Tên | A to Z | Z to A |
| Kích thước | Smallest First | Largest First |

#### 3.1.4 Grid View
```
┌─────┬─────┬─────┐
│ 📷  │ 📷  │ 📷  │  ← 3 columns
├─────┼─────┼─────┤
│ 📷  │ 📷  │ 📷  │  ← Aspect ratio 1:1
├─────┼─────┼─────┤
│ 📷  │ 📷  │ 📷  │  ← Gap: 2dp
└─────┴─────┴─────┘
```

**Specifications:**
- Column count: 3
- Item spacing: 2dp
- Corner radius: 0dp (edge-to-edge)
- Thumbnail height: 120dp
- Scale type: centerCrop

#### 3.1.5 List View
```
┌─────────────────────────────────────────────────────┐
│ ┌──────┐                                            │
│ │  📷  │  IMG_20260126_143052.jpg                   │
│ │ 60dp │  Jan 26, 2026 • 2.5 MB                 >   │
│ └──────┘                                            │
├─────────────────────────────────────────────────────┤
│ ┌──────┐                                            │
│ │  📷  │  Screenshot_2026-01-25.png                 │
│ │ 60dp │  Jan 25, 2026 • 1.2 MB                 >   │
│ └──────┘                                            │
└─────────────────────────────────────────────────────┘
```

**Specifications:**
- Thumbnail size: 60x60dp
- Thumbnail corner radius: 8dp
- Row padding: 16dp horizontal, 12dp vertical
- Separator: 0.5dp, indent 92dp from left
- Chevron icon: 20dp, color `#C7C7CC`

#### 3.1.6 Empty State
```
┌─────────────────────────────────────────────────────┐
│                                                     │
│                       🖼️                            │
│                   (80dp icon)                       │
│                                                     │
│                   No Photos                         │
│                   (20sp, bold)                      │
│                                                     │
│        Take a photo or import from library          │
│                (15sp, secondary)                    │
│                                                     │
└─────────────────────────────────────────────────────┘
```

#### 3.1.7 FAB (Floating Action Button)
- Position: Bottom-right
- Margin: 20dp right, 24dp bottom
- Size: 56dp
- Background: `#007AFF` (Apple Blue)
- Icon: Camera (white)
- Elevation: 4dp

### 3.2 Chụp ảnh

#### 3.2.1 Luồng xử lý
```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Tap FAB    │ ──► │  Check       │ ──► │  Open       │
│  Camera     │     │  Permission  │     │  Camera     │
└─────────────┘     └──────────────┘     └─────────────┘
                                               │
┌─────────────┐     ┌──────────────┐           │
│  Refresh    │ ◄── │  Save to     │ ◄─────────┘
│  Gallery    │     │  MediaStore  │
└─────────────┘     └──────────────┘
```

#### 3.2.2 Lưu ảnh
- Format: JPEG
- Naming: `IMG_yyyyMMdd_HHmmss.jpg`
- Location: `Pictures/Photos/`
- Sử dụng MediaStore API (Android 10+)

### 3.3 Interactions

| Action | Trigger | Result |
|--------|---------|--------|
| Xem ảnh | Tap on photo | Open PhotoViewerActivity |
| Context menu | Long press | Show options (Delete, Share, Add to Album, Hide, Favorite) |
| Multi-select | Long press → Drag | Enable selection mode |

---

## 4. Module Xem ảnh

### 4.1 PhotoViewerActivity

#### 4.1.1 Layout Structure
```
┌─────────────────────────────────────────────────────┐
│ ◄ Back                              ⋮ More Options  │ ← Toolbar (ẩn/hiện)
├─────────────────────────────────────────────────────┤
│                                                     │
│                                                     │
│                                                     │
│                    [  PHOTO  ]                      │ ← ViewPager2
│                                                     │
│                                                     │
│                                                     │
├─────────────────────────────────────────────────────┤
│  ♡ Favorite  │  ✏️ Edit  │  📤 Share  │  🗑️ Delete │ ← Bottom Actions
└─────────────────────────────────────────────────────┘
```

#### 4.1.2 Gestures

| Gesture | Action |
|---------|--------|
| Single tap | Toggle toolbar visibility |
| Double tap | Zoom in/out (toggle 1x ↔ 2x) |
| Pinch | Zoom in/out (1x - 5x) |
| Swipe left/right | Previous/Next photo |
| Swipe down | Close viewer (với animation) |
| Long press | Show context menu |

#### 4.1.3 Zoom Specifications
```java
// Zoom levels
MIN_ZOOM = 1.0f;
MEDIUM_ZOOM = 2.0f;
MAX_ZOOM = 5.0f;

// Double tap behavior
if (currentZoom == MIN_ZOOM) {
    zoomTo(MEDIUM_ZOOM);
} else {
    zoomTo(MIN_ZOOM);
}
```

#### 4.1.4 Photo Info Dialog
```
┌─────────────────────────────────────────────────────┐
│                    Photo Details                     │
├─────────────────────────────────────────────────────┤
│  📷 File Name                                       │
│     IMG_20260126_143052.jpg                         │
├─────────────────────────────────────────────────────┤
│  📅 Date Taken                                      │
│     January 26, 2026 at 2:30 PM                     │
├─────────────────────────────────────────────────────┤
│  📐 Dimensions                                      │
│     4032 × 3024 pixels                              │
├─────────────────────────────────────────────────────┤
│  💾 File Size                                       │
│     2.5 MB                                          │
├─────────────────────────────────────────────────────┤
│  📍 Location (if available)                         │
│     Ho Chi Minh City, Vietnam                       │
├─────────────────────────────────────────────────────┤
│  📱 Device                                          │
│     Samsung Galaxy S24 Ultra                        │
└─────────────────────────────────────────────────────┘
```

### 4.2 ViewPager Implementation

```java
// PhotoPagerAdapter
class PhotoPagerAdapter extends FragmentStateAdapter {
    private List<Photo> photos;
    
    @Override
    public Fragment createFragment(int position) {
        return PhotoFragment.newInstance(photos.get(position));
    }
}

// PhotoFragment với PhotoView library
// Sử dụng: com.github.chrisbanes:PhotoView:2.3.0
```

---

## 5. Module Chỉnh sửa ảnh

### 5.1 PhotoEditorActivity

#### 5.1.1 Layout Structure
```
┌─────────────────────────────────────────────────────┐
│ ✕ Cancel                                     Save ✓ │
├─────────────────────────────────────────────────────┤
│                                                     │
│                                                     │
│                   [  PREVIEW  ]                     │
│                                                     │
│                                                     │
├─────────────────────────────────────────────────────┤
│  🔄 Rotate  │  🎨 Filter  │  ✏️ Brush  │  ✂️ Crop   │
├─────────────────────────────────────────────────────┤
│                                                     │
│              [ Tool Options Panel ]                 │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### 5.2 Rotate Tool

#### 5.2.1 Options
| Button | Action |
|--------|--------|
| Rotate Left | Xoay -90° |
| Rotate Right | Xoay +90° |
| Flip Horizontal | Lật ngang |
| Flip Vertical | Lật dọc |

#### 5.2.2 Implementation
```java
// Rotation
Matrix matrix = new Matrix();
matrix.postRotate(90);
Bitmap rotated = Bitmap.createBitmap(original, 0, 0, 
    original.getWidth(), original.getHeight(), matrix, true);

// Flip
Matrix flipMatrix = new Matrix();
flipMatrix.preScale(-1, 1); // Horizontal flip
```

### 5.3 Filter Tool

#### 5.3.1 Danh sách Filter (10 filters)

| # | Filter Name | Mô tả | ColorMatrix |
|---|-------------|-------|-------------|
| 1 | **No Effect** | Ảnh gốc | Identity matrix |
| 2 | **Grayscale** | Đen trắng | Saturation = 0 |
| 3 | **Vintage** | Hiệu ứng cổ điển | Sepia tone + contrast |
| 4 | **Cream** | Tone kem ấm | Warm temperature |
| 5 | **Forest** | Tone xanh lá | Green tint |
| 6 | **Cozy** | Ấm áp, contrast thấp | Low contrast + warm |
| 7 | **Blossom** | Tone hồng nhẹ | Pink overlay |
| 8 | **Evergreen** | Xanh đậm, tươi | Enhanced green |
| 9 | **Auto** | Tự động cân bằng | Auto levels |
| 10 | **Sharpen** | Làm nét | Convolution matrix |

#### 5.3.2 Filter Preview UI
```
┌─────────────────────────────────────────────────────┐
│  ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐          │
│  │ 📷  │ │ 📷  │ │ 📷  │ │ 📷  │ │ 📷  │  ← Scroll │
│  │     │ │     │ │     │ │     │ │     │           │
│  └──┬──┘ └──┬──┘ └──┬──┘ └──┬──┘ └──┬──┘          │
│   None  Grayscale Vintage Cream  Forest           │
└─────────────────────────────────────────────────────┘
```

#### 5.3.3 Filter Implementation Example
```java
// Grayscale Filter
ColorMatrix grayscaleMatrix = new ColorMatrix();
grayscaleMatrix.setSaturation(0);

// Vintage Filter
float[] vintage = {
    0.9f, 0.5f, 0.1f, 0, 0,    // Red
    0.3f, 0.8f, 0.1f, 0, 0,    // Green
    0.2f, 0.3f, 0.5f, 0, 0,    // Blue
    0,    0,    0,    1, 0     // Alpha
};
ColorMatrix vintageMatrix = new ColorMatrix(vintage);

// Apply filter
Paint paint = new Paint();
paint.setColorFilter(new ColorMatrixColorFilter(matrix));
canvas.drawBitmap(bitmap, 0, 0, paint);
```

### 5.4 Brush Tool

#### 5.4.1 Brush Options Panel
```
┌─────────────────────────────────────────────────────┐
│  Brush Size:  ○───────●───────○  (5-50dp)          │
├─────────────────────────────────────────────────────┤
│  Colors:                                            │
│  ● ● ● ● ● ● ● ● ● ●                               │
│  🔴🟠🟡🟢🔵🟣⚫⚪🟤                                   │
├─────────────────────────────────────────────────────┤
│  Opacity:  ○─────────●─────○  (20-100%)            │
├─────────────────────────────────────────────────────┤
│  [ Undo ]  [ Clear All ]  [ Eraser ]               │
└─────────────────────────────────────────────────────┘
```

#### 5.4.2 Color Palette
```java
int[] BRUSH_COLORS = {
    Color.RED,        // #FF0000
    Color.parseColor("#FF9500"),  // Orange
    Color.YELLOW,     // #FFFF00
    Color.GREEN,      // #00FF00
    Color.BLUE,       // #0000FF
    Color.parseColor("#AF52DE"),  // Purple
    Color.BLACK,      // #000000
    Color.WHITE,      // #FFFFFF
    Color.parseColor("#8B4513"),  // Brown
    Color.parseColor("#FF2D55"),  // Pink
};
```

#### 5.4.3 Drawing Implementation
```java
public class DrawingView extends View {
    private Path currentPath;
    private Paint drawPaint;
    private List<DrawingPath> paths = new ArrayList<>();
    
    @Override
    protected void onDraw(Canvas canvas) {
        // Draw all saved paths
        for (DrawingPath dp : paths) {
            canvas.drawPath(dp.path, dp.paint);
        }
        // Draw current path
        canvas.drawPath(currentPath, drawPaint);
    }
    
    @Override
    public boolean onTouchEvent(MotionEvent event) {
        float x = event.getX();
        float y = event.getY();
        
        switch (event.getAction()) {
            case MotionEvent.ACTION_DOWN:
                currentPath.moveTo(x, y);
                break;
            case MotionEvent.ACTION_MOVE:
                currentPath.lineTo(x, y);
                break;
            case MotionEvent.ACTION_UP:
                paths.add(new DrawingPath(currentPath, drawPaint));
                currentPath = new Path();
                break;
        }
        invalidate();
        return true;
    }
    
    public void undo() {
        if (!paths.isEmpty()) {
            paths.remove(paths.size() - 1);
            invalidate();
        }
    }
}
```

### 5.5 Crop Tool

#### 5.5.1 Aspect Ratio Options
| Option | Ratio |
|--------|-------|
| Free | No constraint |
| Square | 1:1 |
| Portrait | 3:4 |
| Landscape | 4:3 |
| Widescreen | 16:9 |
| Story | 9:16 |

#### 5.5.2 Crop UI
```
┌─────────────────────────────────────────────────────┐
│                                                     │
│     ┌─────────────────────────────┐                │
│     │ ○─────────────────────────○ │ ← Resize handles│
│     │ │                         │ │                │
│     │ │      [CROP AREA]        │ │ ← Draggable    │
│     │ │                         │ │                │
│     │ ○─────────────────────────○ │                │
│     └─────────────────────────────┘                │
│                                                     │
├─────────────────────────────────────────────────────┤
│  Free │ 1:1 │ 3:4 │ 4:3 │ 16:9 │ 9:16            │
└─────────────────────────────────────────────────────┘
```

### 5.6 Save Edited Photo

#### 5.6.1 Save Options Dialog
```
┌─────────────────────────────────────────────────────┐
│                    Save Photo                        │
├─────────────────────────────────────────────────────┤
│  ○ Save as new photo                                │
│  ○ Overwrite original                               │
├─────────────────────────────────────────────────────┤
│  Quality: High (95%)  ▼                             │
├─────────────────────────────────────────────────────┤
│           [ Cancel ]     [ Save ]                   │
└─────────────────────────────────────────────────────┘
```

---

## 6. Module Album

### 6.1 Albums Screen

#### 6.1.1 Layout
```
┌─────────────────────────────────────────────────────┐
│                      Albums                          │
│                    12 Albums                         │
├─────────────────────────────────────────────────────┤
│  📁 My Albums                              + Create │
├─────────────────────────────────────────────────────┤
│ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐    │
│ │   ████████  │ │   ████████  │ │   ████████  │    │
│ │   ████████  │ │   ████████  │ │   ████████  │    │
│ │   ████████  │ │   ████████  │ │   ████████  │    │
│ ├─────────────┤ ├─────────────┤ ├─────────────┤    │
│ │ Travel      │ │ Family      │ │ Work        │    │
│ │ 45 photos   │ │ 128 photos  │ │ 23 photos   │    │
│ └─────────────┘ └─────────────┘ └─────────────┘    │
├─────────────────────────────────────────────────────┤
│  🔒 System Albums                                   │
├─────────────────────────────────────────────────────┤
│ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐    │
│ │   ⭐⭐⭐    │ │   🗑️🗑️🗑️   │ │   🔒🔒🔒    │    │
│ ├─────────────┤ ├─────────────┤ ├─────────────┤    │
│ │ Favorites   │ │ Trash       │ │ Hidden      │    │
│ │ 67 photos   │ │ 12 photos   │ │ 🔐 Locked   │    │
│ └─────────────┘ └─────────────┘ └─────────────┘    │
└─────────────────────────────────────────────────────┘
```

### 6.2 Album Item Design

```
┌─────────────────────┐
│ ┌─────────────────┐ │ ← Cover photo (stacked effect)
│ │┌───────────────┐│ │
│ ││               ││ │
│ ││    COVER      ││ │
│ ││    PHOTO      ││ │
│ ││               ││ │
│ │└───────────────┘│ │
│ └─────────────────┘ │
├─────────────────────┤
│ Album Name          │ ← 15sp, bold
│ 45 photos           │ ← 13sp, secondary
└─────────────────────┘
```

### 6.3 System Albums (Default)

| Album | Icon | Mô tả | Editable |
|-------|------|-------|----------|
| **Favorites** | ⭐ | Ảnh được đánh dấu yêu thích | Không xóa được |
| **Trash** | 🗑️ | Ảnh đã xóa (giữ 30 ngày) | Không xóa được |
| **Hidden** | 🔒 | Ảnh ẩn, cần mật khẩu | Không xóa được |

### 6.4 Create Album Flow

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Tap +      │ ──► │  Enter       │ ──► │  Select     │
│  Create     │     │  Album Name  │     │  Photos     │
└─────────────┘     └──────────────┘     └─────────────┘
                                               │
                    ┌──────────────┐           │
                    │  Album       │ ◄─────────┘
                    │  Created ✓   │
                    └──────────────┘
```

#### 6.4.1 Create Album Dialog
```
┌─────────────────────────────────────────────────────┐
│                   New Album                          │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Album Name                                         │
│  ┌─────────────────────────────────────────────┐   │
│  │ Summer Vacation 2026                        │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
├─────────────────────────────────────────────────────┤
│           [ Cancel ]     [ Create ]                 │
└─────────────────────────────────────────────────────┘
```

### 6.5 Album Detail Screen

```
┌─────────────────────────────────────────────────────┐
│ ◄ Albums              Travel               ⋮ More   │
│                      45 Photos                      │
├─────────────────────────────────────────────────────┤
│ ┌─────┬─────┬─────┐                                │
│ │ 📷  │ 📷  │ 📷  │                                │
│ ├─────┼─────┼─────┤                                │
│ │ 📷  │ 📷  │ 📷  │                                │
│ ├─────┼─────┼─────┤                                │
│ │ 📷  │ 📷  │ 📷  │                                │
│ └─────┴─────┴─────┘                                │
├─────────────────────────────────────────────────────┤
│        [ + Add Photos ]     [ Select ]             │
└─────────────────────────────────────────────────────┘
```

### 6.6 Album Actions

#### 6.6.1 Album Context Menu (Long Press)
```
┌─────────────────────────────────────────────────────┐
│  ✏️  Rename Album                                   │
├─────────────────────────────────────────────────────┤
│  🖼️  Change Cover Photo                            │
├─────────────────────────────────────────────────────┤
│  📤  Share Album                                    │
├─────────────────────────────────────────────────────┤
│  🗑️  Delete Album                                  │
└─────────────────────────────────────────────────────┘
```

### 6.7 Add Photos to Album

#### 6.7.1 Selection Mode
```
┌─────────────────────────────────────────────────────┐
│ ✕ Cancel         Select Photos         Done (12)   │
├─────────────────────────────────────────────────────┤
│ ┌─────┬─────┬─────┐                                │
│ │ 📷✓ │ 📷  │ 📷✓ │  ← Checkmark overlay          │
│ ├─────┼─────┼─────┤                                │
│ │ 📷  │ 📷✓ │ 📷  │                                │
│ ├─────┼─────┼─────┤                                │
│ │ 📷✓ │ 📷✓ │ 📷  │                                │
│ └─────┴─────┴─────┘                                │
└─────────────────────────────────────────────────────┘
```

---

## 7. Module Yêu thích

### 7.1 Favorites Screen

#### 7.1.1 Access
- Tab "Favorites" trong Bottom Navigation
- Hoặc từ System Albums

#### 7.1.2 Layout
```
┌─────────────────────────────────────────────────────┐
│                    Favorites                         │
│                    ⭐ 67 Photos                      │
├─────────────────────────────────────────────────────┤
│ ┌─────┬─────┬─────┐                                │
│ │ 📷⭐│ 📷⭐│ 📷⭐│                                │
│ ├─────┼─────┼─────┤                                │
│ │ 📷⭐│ 📷⭐│ 📷⭐│                                │
│ └─────┴─────┴─────┘                                │
└─────────────────────────────────────────────────────┘
```

### 7.2 Favorite Actions

| Action | Trigger | Animation |
|--------|---------|-----------|
| Add to Favorites | Tap ♡ icon | ♡ → ❤️ (scale + bounce) |
| Remove from Favorites | Tap ❤️ icon | ❤️ → ♡ (fade) |
| Quick Favorite | Double tap on photo | Heart popup animation |

### 7.3 Database Schema

```sql
-- Photo table has is_favorite column
ALTER TABLE photos ADD COLUMN is_favorite INTEGER DEFAULT 0;

-- Query favorites
SELECT * FROM photos WHERE is_favorite = 1 ORDER BY favorite_date DESC;
```

---

## 8. Module Thùng rác

### 8.1 Trash Screen

```
┌─────────────────────────────────────────────────────┐
│                      Trash                           │
│                   🗑️ 12 Photos                       │
│         Items will be deleted after 30 days         │
├─────────────────────────────────────────────────────┤
│ ┌─────┬─────┬─────┐                                │
│ │ 📷  │ 📷  │ 📷  │                                │
│ │ 28d │ 15d │ 7d  │  ← Days remaining              │
│ ├─────┼─────┼─────┤                                │
│ │ 📷  │ 📷  │ 📷  │                                │
│ │ 5d  │ 3d  │ 1d  │                                │
│ └─────┴─────┴─────┘                                │
├─────────────────────────────────────────────────────┤
│  [ Restore All ]         [ Empty Trash ]           │
└─────────────────────────────────────────────────────┘
```

### 8.2 Trash Flow

```
                    ┌─────────────┐
                    │   Photo     │
                    └──────┬──────┘
                           │ Delete
                           ▼
                    ┌─────────────┐
                    │   Trash     │ ← Giữ 30 ngày
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
       ┌───────────┐ ┌──────────┐ ┌──────────┐
       │  Restore  │ │  30 days │ │  Delete  │
       │           │ │  auto    │ │  Forever │
       └───────────┘ └──────────┘ └──────────┘
              │            │            │
              ▼            ▼            ▼
       ┌───────────┐ ┌──────────────────────┐
       │  Gallery  │ │   Permanently        │
       │           │ │   Deleted            │
       └───────────┘ └──────────────────────┘
```

### 8.3 Trash Actions

#### 8.3.1 Single Photo Actions
```
┌─────────────────────────────────────────────────────┐
│  ↩️  Restore Photo                                  │
├─────────────────────────────────────────────────────┤
│  🗑️  Delete Permanently                            │
└─────────────────────────────────────────────────────┘
```

#### 8.3.2 Confirmation Dialogs

**Delete Permanently:**
```
┌─────────────────────────────────────────────────────┐
│              Delete Permanently?                     │
├─────────────────────────────────────────────────────┤
│  This photo will be permanently deleted.            │
│  This action cannot be undone.                      │
├─────────────────────────────────────────────────────┤
│        [ Cancel ]     [ Delete Forever ]            │
└─────────────────────────────────────────────────────┘
```

**Empty Trash:**
```
┌─────────────────────────────────────────────────────┐
│               Empty Trash?                           │
├─────────────────────────────────────────────────────┤
│  All 12 photos will be permanently deleted.         │
│  This action cannot be undone.                      │
├─────────────────────────────────────────────────────┤
│        [ Cancel ]     [ Empty Trash ]               │
└─────────────────────────────────────────────────────┘
```

### 8.4 Auto-delete Implementation

```java
// WorkManager scheduled task
public class TrashCleanupWorker extends Worker {
    
    @Override
    public Result doWork() {
        long thirtyDaysAgo = System.currentTimeMillis() - (30L * 24 * 60 * 60 * 1000);
        
        // Delete photos older than 30 days in trash
        photoDao.deleteOldTrashPhotos(thirtyDaysAgo);
        
        return Result.success();
    }
}

// Schedule daily cleanup
PeriodicWorkRequest cleanupRequest = 
    new PeriodicWorkRequest.Builder(TrashCleanupWorker.class, 1, TimeUnit.DAYS)
        .build();
WorkManager.getInstance(context).enqueue(cleanupRequest);
```

---

## 9. Module Ảnh ẩn

### 9.1 Hidden Photos Flow

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  First      │ ──► │  Set         │ ──► │  Confirm    │
│  Access     │     │  Password    │     │  Password   │
└─────────────┘     └──────────────┘     └─────────────┘

┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Subsequent │ ──► │  Enter       │ ──► │  View       │
│  Access     │     │  Password    │     │  Hidden     │
└─────────────┘     └──────────────┘     └─────────────┘
```

### 9.2 Set Password Screen

```
┌─────────────────────────────────────────────────────┐
│                  🔒 Set Password                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Create a password to protect your hidden photos    │
│                                                     │
│  New Password                                       │
│  ┌─────────────────────────────────────────────┐   │
│  │ ●●●●●●                                      │   │
│  └─────────────────────────────────────────────┘   │
│  Must be at least 4 characters                     │
│                                                     │
│  Confirm Password                                  │
│  ┌─────────────────────────────────────────────┐   │
│  │ ●●●●●●                                      │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
├─────────────────────────────────────────────────────┤
│                   [ Set Password ]                  │
└─────────────────────────────────────────────────────┘
```

### 9.3 Enter Password Screen

```
┌─────────────────────────────────────────────────────┐
│                  🔒 Hidden Photos                    │
├─────────────────────────────────────────────────────┤
│                                                     │
│                      🔐                             │
│                                                     │
│            Enter your password                      │
│                                                     │
│           ┌───┬───┬───┬───┬───┬───┐               │
│           │ ● │ ● │ ● │ ● │ ○ │ ○ │               │
│           └───┴───┴───┴───┴───┴───┘               │
│                                                     │
│  ┌───┬───┬───┐                                     │
│  │ 1 │ 2 │ 3 │                                     │
│  ├───┼───┼───┤                                     │
│  │ 4 │ 5 │ 6 │   ← Custom numeric keypad          │
│  ├───┼───┼───┤                                     │
│  │ 7 │ 8 │ 9 │                                     │
│  ├───┼───┼───┤                                     │
│  │   │ 0 │ ⌫ │                                     │
│  └───┴───┴───┘                                     │
│                                                     │
│            Forgot Password?                         │
└─────────────────────────────────────────────────────┘
```

### 9.4 Password Security

#### 9.4.1 SHA-256 Hashing
```java
public class PasswordUtils {
    
    public static String hashPassword(String password) {
        try {
            MessageDigest digest = MessageDigest.getInstance("SHA-256");
            byte[] hash = digest.digest(password.getBytes(StandardCharsets.UTF_8));
            
            // Convert to hex string
            StringBuilder hexString = new StringBuilder();
            for (byte b : hash) {
                String hex = Integer.toHexString(0xff & b);
                if (hex.length() == 1) hexString.append('0');
                hexString.append(hex);
            }
            return hexString.toString();
        } catch (NoSuchAlgorithmException e) {
            throw new RuntimeException(e);
        }
    }
    
    public static boolean verifyPassword(String input, String storedHash) {
        return hashPassword(input).equals(storedHash);
    }
}
```

#### 9.4.2 Storage
```java
// SharedPreferences (encrypted)
EncryptedSharedPreferences prefs = EncryptedSharedPreferences.create(
    "hidden_prefs",
    MasterKeys.getOrCreate(MasterKeys.AES256_GCM_SPEC),
    context,
    EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
    EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
);

prefs.edit().putString("password_hash", hashedPassword).apply();
```

### 9.5 Change Password Flow

```
┌─────────────────────────────────────────────────────┐
│              Change Password                         │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Current Password                                   │
│  ┌─────────────────────────────────────────────┐   │
│  │ ●●●●●●                                      │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
│  New Password                                       │
│  ┌─────────────────────────────────────────────┐   │
│  │ ●●●●●●●●                                    │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
│  Confirm New Password                              │
│  ┌─────────────────────────────────────────────┐   │
│  │ ●●●●●●●●                                    │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
├─────────────────────────────────────────────────────┤
│         [ Cancel ]     [ Change Password ]          │
└─────────────────────────────────────────────────────┘
```

### 9.6 Hide/Unhide Photo

#### 9.6.1 Hide Photo
```
Photo Context Menu:
┌─────────────────────────────────────────────────────┐
│  🔒  Hide Photo                                     │
└─────────────────────────────────────────────────────┘

Confirmation:
┌─────────────────────────────────────────────────────┐
│              Hide this photo?                        │
├─────────────────────────────────────────────────────┤
│  This photo will be moved to Hidden album.          │
│  You'll need your password to view it.              │
├─────────────────────────────────────────────────────┤
│          [ Cancel ]     [ Hide ]                    │
└─────────────────────────────────────────────────────┘
```

---

## 10. Module Slideshow

### 10.1 Slideshow Screen

```
┌─────────────────────────────────────────────────────┐
│                                                     │
│                                                     │
│                                                     │
│                   [  PHOTO  ]                       │ ← Full screen
│                                                     │
│                                                     │
│                                                     │
├─────────────────────────────────────────────────────┤
│  ▶️/⏸️  │  ◀◀  │  ▶▶  │  ⚙️ Settings  │  ✕ Exit   │
├─────────────────────────────────────────────────────┤
│  ●○○○○○○○○○○○○○○○○○○○○○○                          │ ← Progress dots
│                    3 / 45                           │
└─────────────────────────────────────────────────────┘
```

### 10.2 Slideshow Settings

```
┌─────────────────────────────────────────────────────┐
│              Slideshow Settings                      │
├─────────────────────────────────────────────────────┤
│                                                     │
│  ⏱️ Duration per slide                             │
│  ○ 2 seconds                                        │
│  ● 3 seconds (default)                              │
│  ○ 5 seconds                                        │
│  ○ 10 seconds                                       │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│  🔄 Transition Effect                               │
│  ○ None                                             │
│  ● Fade (default)                                   │
│  ○ Slide                                            │
│  ○ Zoom                                             │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│  🔁 Loop                                           │
│  ┌────────────────────────────────────────[●]─┐    │
│                                            ON      │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│  🔀 Shuffle                                        │
│  ┌────[○]────────────────────────────────────┐    │
│      OFF                                           │
│                                                     │
├─────────────────────────────────────────────────────┤
│                      [ Done ]                       │
└─────────────────────────────────────────────────────┘
```

### 10.3 Slideshow Implementation

```java
public class SlideshowActivity extends AppCompatActivity {
    
    private Handler slideshowHandler = new Handler(Looper.getMainLooper());
    private int currentIndex = 0;
    private long intervalMs = 3000; // 3 seconds default
    private boolean isPlaying = true;
    private boolean isLoop = true;
    private boolean isShuffle = false;
    
    private Runnable slideshowRunnable = new Runnable() {
        @Override
        public void run() {
            if (isPlaying) {
                showNextPhoto();
                slideshowHandler.postDelayed(this, intervalMs);
            }
        }
    };
    
    private void showNextPhoto() {
        if (isShuffle) {
            currentIndex = new Random().nextInt(photos.size());
        } else {
            currentIndex++;
            if (currentIndex >= photos.size()) {
                if (isLoop) {
                    currentIndex = 0;
                } else {
                    stopSlideshow();
                    return;
                }
            }
        }
        
        // Apply transition animation
        applyTransition();
        viewPager.setCurrentItem(currentIndex, true);
    }
    
    private void applyTransition() {
        switch (transitionType) {
            case FADE:
                viewPager.setPageTransformer(new FadePageTransformer());
                break;
            case SLIDE:
                viewPager.setPageTransformer(new SlidePageTransformer());
                break;
            case ZOOM:
                viewPager.setPageTransformer(new ZoomPageTransformer());
                break;
        }
    }
}
```

### 10.4 Transition Animations

```java
// Fade Transition
public class FadePageTransformer implements ViewPager2.PageTransformer {
    @Override
    public void transformPage(@NonNull View page, float position) {
        page.setAlpha(1 - Math.abs(position));
    }
}

// Zoom Transition
public class ZoomPageTransformer implements ViewPager2.PageTransformer {
    private static final float MIN_SCALE = 0.85f;
    
    @Override
    public void transformPage(@NonNull View page, float position) {
        float scaleFactor = Math.max(MIN_SCALE, 1 - Math.abs(position) * 0.15f);
        page.setScaleX(scaleFactor);
        page.setScaleY(scaleFactor);
        page.setAlpha(1 - Math.abs(position));
    }
}
```

---

## 11. Module Tải ảnh từ URL

### 11.1 Import from URL Screen

```
┌─────────────────────────────────────────────────────┐
│ ◄ Back          Import from URL                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│  🌐 Enter image URL                                │
│  ┌─────────────────────────────────────────────┐   │
│  │ https://example.com/image.jpg               │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
│                  [ Preview ]                        │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│            ┌─────────────────────┐                 │
│            │                     │                 │
│            │    [ PREVIEW ]      │ ← Image preview │
│            │                     │                 │
│            └─────────────────────┘                 │
│                                                     │
│  File size: 2.5 MB                                 │
│  Dimensions: 1920 × 1080                           │
│                                                     │
├─────────────────────────────────────────────────────┤
│                   [ Download ]                      │
└─────────────────────────────────────────────────────┘
```

### 11.2 Download Flow

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Enter URL  │ ──► │  Check       │ ──► │  Validate   │
│             │     │  Connection  │     │  URL        │
└─────────────┘     └──────────────┘     └─────────────┘
                           │                    │
                           ▼                    ▼
                    ┌──────────────┐     ┌─────────────┐
                    │  No Network  │     │  Preview    │
                    │  Error       │     │  Image      │
                    └──────────────┘     └──────┬──────┘
                                               │
                    ┌──────────────┐           │
                    │  Saved to    │ ◄─────────┘
                    │  Gallery ✓   │
                    └──────────────┘
```

### 11.3 Network Check

```java
public class NetworkUtils {
    
    public static boolean isNetworkAvailable(Context context) {
        ConnectivityManager cm = (ConnectivityManager) 
            context.getSystemService(Context.CONNECTIVITY_SERVICE);
        
        if (cm != null) {
            NetworkCapabilities capabilities = 
                cm.getNetworkCapabilities(cm.getActiveNetwork());
            return capabilities != null && (
                capabilities.hasTransport(NetworkCapabilities.TRANSPORT_WIFI) ||
                capabilities.hasTransport(NetworkCapabilities.TRANSPORT_CELLULAR) ||
                capabilities.hasTransport(NetworkCapabilities.TRANSPORT_ETHERNET)
            );
        }
        return false;
    }
}
```

### 11.4 URL Validation

```java
public static boolean isValidImageUrl(String url) {
    if (url == null || url.isEmpty()) return false;
    
    // Check URL format
    if (!Patterns.WEB_URL.matcher(url).matches()) return false;
    
    // Check image extension
    String lowerUrl = url.toLowerCase();
    return lowerUrl.endsWith(".jpg") || 
           lowerUrl.endsWith(".jpeg") || 
           lowerUrl.endsWith(".png") || 
           lowerUrl.endsWith(".gif") || 
           lowerUrl.endsWith(".webp") ||
           lowerUrl.endsWith(".bmp");
}
```

### 11.5 Download Implementation

```java
// Using Glide to download and save
Glide.with(context)
    .asBitmap()
    .load(imageUrl)
    .into(new CustomTarget<Bitmap>() {
        @Override
        public void onResourceReady(Bitmap bitmap, Transition<? super Bitmap> transition) {
            saveBitmapToGallery(bitmap);
        }
        
        @Override
        public void onLoadCleared(Drawable placeholder) {}
    });

private void saveBitmapToGallery(Bitmap bitmap) {
    String fileName = "IMG_" + System.currentTimeMillis() + ".jpg";
    
    ContentValues values = new ContentValues();
    values.put(MediaStore.Images.Media.DISPLAY_NAME, fileName);
    values.put(MediaStore.Images.Media.MIME_TYPE, "image/jpeg");
    values.put(MediaStore.Images.Media.RELATIVE_PATH, "Pictures/Photos");
    
    Uri uri = getContentResolver().insert(
        MediaStore.Images.Media.EXTERNAL_CONTENT_URI, values);
    
    try (OutputStream out = getContentResolver().openOutputStream(uri)) {
        bitmap.compress(Bitmap.CompressFormat.JPEG, 95, out);
    }
}
```

---

## 12. Module Giao diện

### 12.1 Theme Support

#### 12.1.1 Light Mode
```xml
<!-- colors.xml (values) -->
<color name="background_primary">#FFFFFF</color>
<color name="background_secondary">#F2F2F7</color>
<color name="text_primary">#1C1C1E</color>
<color name="text_secondary">#8E8E93</color>
<color name="system_blue">#007AFF</color>
<color name="separator">#E5E5EA</color>
```

#### 12.1.2 Dark Mode
```xml
<!-- colors.xml (values-night) -->
<color name="background_primary">#000000</color>
<color name="background_secondary">#1C1C1E</color>
<color name="text_primary">#FFFFFF</color>
<color name="text_secondary">#8E8E93</color>
<color name="system_blue">#0A84FF</color>
<color name="separator">#38383A</color>
```

### 12.2 Settings Screen

```
┌─────────────────────────────────────────────────────┐
│                     Settings                         │
├─────────────────────────────────────────────────────┤
│  🎨 APPEARANCE                                      │
├─────────────────────────────────────────────────────┤
│  🌙 Dark Mode                                   [●] │
│     Automatically switch based on system           │
├─────────────────────────────────────────────────────┤
│  🔢 Grid Columns                                   │
│     ○ 3 (default)  ○ 4  ○ 5                        │
├─────────────────────────────────────────────────────┤
│  🔒 PRIVACY                                        │
├─────────────────────────────────────────────────────┤
│  🔑 Change Hidden Password                      >  │
├─────────────────────────────────────────────────────┤
│  🗑️ Empty Trash                                 >  │
├─────────────────────────────────────────────────────┤
│  📁 STORAGE                                        │
├─────────────────────────────────────────────────────┤
│  💾 Clear Cache                            1.2 GB  │
├─────────────────────────────────────────────────────┤
│  ℹ️ ABOUT                                          │
├─────────────────────────────────────────────────────┤
│  📱 Version                                  1.0.0 │
├─────────────────────────────────────────────────────┤
│  📄 Privacy Policy                              >  │
├─────────────────────────────────────────────────────┤
│  📄 Terms of Service                            >  │
└─────────────────────────────────────────────────────┘
```

### 12.3 Theme Switching

```java
public class ThemeManager {
    private static final String PREF_THEME = "theme_mode";
    
    public static void setTheme(Context context, int mode) {
        SharedPreferences prefs = PreferenceManager.getDefaultSharedPreferences(context);
        prefs.edit().putInt(PREF_THEME, mode).apply();
        AppCompatDelegate.setDefaultNightMode(mode);
    }
    
    public static void applyTheme(Context context) {
        SharedPreferences prefs = PreferenceManager.getDefaultSharedPreferences(context);
        int mode = prefs.getInt(PREF_THEME, AppCompatDelegate.MODE_NIGHT_FOLLOW_SYSTEM);
        AppCompatDelegate.setDefaultNightMode(mode);
    }
}

// Usage
ThemeManager.setTheme(context, AppCompatDelegate.MODE_NIGHT_YES);  // Dark
ThemeManager.setTheme(context, AppCompatDelegate.MODE_NIGHT_NO);   // Light
ThemeManager.setTheme(context, AppCompatDelegate.MODE_NIGHT_FOLLOW_SYSTEM); // Auto
```

---

## 13. Module Chia sẻ

### 13.1 Share Options

```
┌─────────────────────────────────────────────────────┐
│                    Share Photo                       │
├─────────────────────────────────────────────────────┤
│                                                     │
│  ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐         │
│  │ 💬  │ │ 📧  │ │ 📘  │ │ 📸  │ │ 🐦  │         │
│  │Mess │ │Email│ │ FB  │ │Insta│ │ X   │         │
│  └─────┘ └─────┘ └─────┘ └─────┘ └─────┘         │
│                                                     │
│  ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐         │
│  │ 💾  │ │ 📋  │ │ 🖨️  │ │ ☁️  │ │ ⋯  │         │
│  │Save │ │Copy │ │Print│ │Drive│ │More │         │
│  └─────┘ └─────┘ └─────┘ └─────┘ └─────┘         │
│                                                     │
├─────────────────────────────────────────────────────┤
│  🖼️ Set as Wallpaper                               │
├─────────────────────────────────────────────────────┤
│           [ Cancel ]                                │
└─────────────────────────────────────────────────────┘
```

### 13.2 Share Implementation

```java
public class ShareUtils {
    
    public static void sharePhoto(Context context, Photo photo) {
        File file = new File(photo.getPath());
        Uri uri = FileProvider.getUriForFile(context,
            context.getPackageName() + ".fileprovider", file);
        
        Intent shareIntent = new Intent(Intent.ACTION_SEND);
        shareIntent.setType("image/*");
        shareIntent.putExtra(Intent.EXTRA_STREAM, uri);
        shareIntent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
        
        context.startActivity(Intent.createChooser(shareIntent, "Share Photo"));
    }
    
    public static void shareMultiplePhotos(Context context, List<Photo> photos) {
        ArrayList<Uri> uris = new ArrayList<>();
        for (Photo photo : photos) {
            File file = new File(photo.getPath());
            Uri uri = FileProvider.getUriForFile(context,
                context.getPackageName() + ".fileprovider", file);
            uris.add(uri);
        }
        
        Intent shareIntent = new Intent(Intent.ACTION_SEND_MULTIPLE);
        shareIntent.setType("image/*");
        shareIntent.putParcelableArrayListExtra(Intent.EXTRA_STREAM, uris);
        shareIntent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
        
        context.startActivity(Intent.createChooser(shareIntent, "Share Photos"));
    }
}
```

### 13.3 Set as Wallpaper

```java
public static void setAsWallpaper(Context context, Photo photo) {
    try {
        Uri uri = Uri.parse("file://" + photo.getPath());
        
        Intent intent = new Intent(Intent.ACTION_ATTACH_DATA);
        intent.addCategory(Intent.CATEGORY_DEFAULT);
        intent.setDataAndType(uri, "image/*");
        intent.putExtra("mimeType", "image/*");
        intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
        
        context.startActivity(Intent.createChooser(intent, "Set as Wallpaper"));
    } catch (Exception e) {
        Toast.makeText(context, "Unable to set wallpaper", Toast.LENGTH_SHORT).show();
    }
}
```

---

## 14. Module AI Features

### 14.1 Tổng quan AI Features

| # | Feature | Technology | Mô tả |
|---|---------|------------|-------|
| 1 | 🏷️ Auto Tagging | ML Kit Image Labeling | Tự động gắn tag cho ảnh |
| 2 | 😀 Face Detection | ML Kit Face Detection | Nhận diện khuôn mặt |
| 3 | 👤 People Album | Face clustering | Nhóm ảnh theo người |
| 4 | 🔍 Smart Search | NLP + Image features | Tìm kiếm bằng ngôn ngữ tự nhiên |
| 5 | 📝 OCR | ML Kit Text Recognition | Nhận diện text trong ảnh |
| 6 | 🖼️ Background Remove | TensorFlow Lite | Xóa background ảnh |
| 7 | ✨ Auto Enhance | ML-based enhancement | Tự động cải thiện chất lượng ảnh |
| 8 | 🏞️ Scene Detection | Image classification | Phân loại cảnh (biển, núi, thành phố...) |

### 14.2 Auto Tagging (ML Kit Image Labeling)

#### 14.2.1 Feature Description
Tự động phân tích ảnh và gắn các tag mô tả nội dung ảnh.

#### 14.2.2 UI
```
┌─────────────────────────────────────────────────────┐
│                    Photo Details                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│  🏷️ AI Tags                                        │
│  ┌─────────────────────────────────────────────┐   │
│  │ 🏖️ Beach  🌊 Ocean  ☀️ Sunny  🌴 Palm Tree │   │
│  │ 🏝️ Island  👙 Swimwear  🐚 Shell           │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
│  Confidence: High (92%)                            │
│                                                     │
└─────────────────────────────────────────────────────┘
```

#### 14.2.3 Implementation
```java
// Add dependency
// implementation 'com.google.mlkit:image-labeling:17.0.7'

public class ImageTagger {
    private final ImageLabeler labeler;
    
    public ImageTagger() {
        ImageLabelerOptions options = new ImageLabelerOptions.Builder()
            .setConfidenceThreshold(0.7f)
            .build();
        labeler = ImageLabeling.getClient(options);
    }
    
    public void tagImage(Bitmap bitmap, OnTagsListener listener) {
        InputImage image = InputImage.fromBitmap(bitmap, 0);
        
        labeler.process(image)
            .addOnSuccessListener(labels -> {
                List<String> tags = new ArrayList<>();
                for (ImageLabel label : labels) {
                    tags.add(label.getText());
                }
                listener.onSuccess(tags);
            })
            .addOnFailureListener(e -> listener.onError(e));
    }
}

// Usage
ImageTagger tagger = new ImageTagger();
tagger.tagImage(bitmap, new OnTagsListener() {
    @Override
    public void onSuccess(List<String> tags) {
        // Save tags to database
        photoDao.updateTags(photoId, tags);
    }
});
```

### 14.3 Face Detection & People Album

#### 14.3.1 Feature Description
- Phát hiện khuôn mặt trong ảnh
- Nhóm các ảnh có cùng người thành album tự động
- Cho phép đặt tên cho từng người

#### 14.3.2 People Album UI
```
┌─────────────────────────────────────────────────────┐
│                      People                          │
├─────────────────────────────────────────────────────┤
│                                                     │
│  ┌───────┐ ┌───────┐ ┌───────┐ ┌───────┐          │
│  │ 👤    │ │ 👤    │ │ 👤    │ │ 👤    │          │
│  │ ●●●●  │ │ ●●●●  │ │ ●●●●  │ │ ●●●●  │          │
│  ├───────┤ ├───────┤ ├───────┤ ├───────┤          │
│  │ John  │ │ Mary  │ │ David │ │Unknown│          │
│  │125 📷 │ │ 89 📷 │ │ 45 📷 │ │ 23 📷 │          │
│  └───────┘ └───────┘ └───────┘ └───────┘          │
│                                                     │
└─────────────────────────────────────────────────────┘
```

#### 14.3.3 Implementation
```java
// Add dependency
// implementation 'com.google.mlkit:face-detection:16.1.5'

public class FaceDetector {
    private final com.google.mlkit.vision.face.FaceDetector detector;
    
    public FaceDetector() {
        FaceDetectorOptions options = new FaceDetectorOptions.Builder()
            .setPerformanceMode(FaceDetectorOptions.PERFORMANCE_MODE_ACCURATE)
            .setContourMode(FaceDetectorOptions.CONTOUR_MODE_ALL)
            .setClassificationMode(FaceDetectorOptions.CLASSIFICATION_MODE_ALL)
            .build();
        detector = FaceDetection.getClient(options);
    }
    
    public void detectFaces(Bitmap bitmap, OnFacesListener listener) {
        InputImage image = InputImage.fromBitmap(bitmap, 0);
        
        detector.process(image)
            .addOnSuccessListener(faces -> {
                List<FaceData> faceDataList = new ArrayList<>();
                for (Face face : faces) {
                    Rect bounds = face.getBoundingBox();
                    Bitmap faceBitmap = Bitmap.createBitmap(
                        bitmap, bounds.left, bounds.top, 
                        bounds.width(), bounds.height()
                    );
                    faceDataList.add(new FaceData(faceBitmap, bounds));
                }
                listener.onSuccess(faceDataList);
            });
    }
}
```

### 14.4 Smart Search

#### 14.4.1 Feature Description
Tìm kiếm ảnh bằng ngôn ngữ tự nhiên.

#### 14.4.2 Examples
| Query | Result |
|-------|--------|
| "photos at beach" | Ảnh có tag beach, ocean, sand |
| "selfies" | Ảnh có face ở center |
| "photos with John" | Ảnh có mặt John |
| "blue sky" | Ảnh có tag sky, blue colors |
| "food photos" | Ảnh có tag food, restaurant |

#### 14.4.3 Search UI
```
┌─────────────────────────────────────────────────────┐
│ ┌─────────────────────────────────────────────────┐ │
│ │ 🔍 Search photos...                             │ │
│ └─────────────────────────────────────────────────┘ │
├─────────────────────────────────────────────────────┤
│  Recent Searches                                    │
│  • beach vacation                                   │
│  • birthday party                                   │
│  • photos with mom                                  │
├─────────────────────────────────────────────────────┤
│  Suggestions                                        │
│  🏖️ Beach  🎂 Birthday  🐕 Dogs  🌸 Flowers       │
└─────────────────────────────────────────────────────┘
```

### 14.5 OCR (Text Recognition)

#### 14.5.1 Feature Description
Nhận diện và trích xuất text từ ảnh (screenshots, documents, etc.)

#### 14.5.2 UI
```
┌─────────────────────────────────────────────────────┐
│                   Detected Text                      │
├─────────────────────────────────────────────────────┤
│                                                     │
│  📝 "Hello World! This is a sample text            │
│      detected from the image. You can copy         │
│      or search using this text."                   │
│                                                     │
├─────────────────────────────────────────────────────┤
│  [ 📋 Copy ]  [ 🔍 Search ]  [ 📤 Share ]          │
└─────────────────────────────────────────────────────┘
```

#### 14.5.3 Implementation
```java
// Add dependency
// implementation 'com.google.mlkit:text-recognition:16.0.0'

public class TextRecognizer {
    private final com.google.mlkit.vision.text.TextRecognizer recognizer;
    
    public TextRecognizer() {
        recognizer = TextRecognition.getClient(TextRecognizerOptions.DEFAULT_OPTIONS);
    }
    
    public void recognizeText(Bitmap bitmap, OnTextListener listener) {
        InputImage image = InputImage.fromBitmap(bitmap, 0);
        
        recognizer.process(image)
            .addOnSuccessListener(text -> {
                listener.onSuccess(text.getText());
            })
            .addOnFailureListener(e -> listener.onError(e));
    }
}
```

### 14.6 Background Removal

#### 14.6.1 Feature Description
Tự động xóa background, giữ lại subject chính.

#### 14.6.2 UI
```
┌─────────────────────────────────────────────────────┐
│ ◄ Back       Remove Background              Done ✓ │
├─────────────────────────────────────────────────────┤
│                                                     │
│  ┌───────────────┐    ┌───────────────┐           │
│  │               │    │               │           │
│  │   ORIGINAL    │ ➜ │   RESULT      │           │
│  │               │    │  (no bg)      │           │
│  └───────────────┘    └───────────────┘           │
│                                                     │
├─────────────────────────────────────────────────────┤
│  Background Color:                                  │
│  ○ Transparent  ● White  ○ Black  ○ Custom        │
├─────────────────────────────────────────────────────┤
│                   [ Save ]                          │
└─────────────────────────────────────────────────────┘
```

#### 14.6.3 Implementation
```java
// Using ML Kit Selfie Segmentation
// implementation 'com.google.mlkit:segmentation-selfie:16.0.0-beta4'

public class BackgroundRemover {
    private final Segmenter segmenter;
    
    public BackgroundRemover() {
        SelfieSegmenterOptions options = new SelfieSegmenterOptions.Builder()
            .setDetectorMode(SelfieSegmenterOptions.SINGLE_IMAGE_MODE)
            .enableRawSizeMask()
            .build();
        segmenter = Segmentation.getClient(options);
    }
    
    public void removeBackground(Bitmap bitmap, int bgColor, OnResultListener listener) {
        InputImage image = InputImage.fromBitmap(bitmap, 0);
        
        segmenter.process(image)
            .addOnSuccessListener(mask -> {
                Bitmap result = applyMask(bitmap, mask, bgColor);
                listener.onSuccess(result);
            });
    }
    
    private Bitmap applyMask(Bitmap original, SegmentationMask mask, int bgColor) {
        ByteBuffer buffer = mask.getBuffer();
        int width = mask.getWidth();
        int height = mask.getHeight();
        
        Bitmap result = Bitmap.createBitmap(width, height, Bitmap.Config.ARGB_8888);
        
        for (int y = 0; y < height; y++) {
            for (int x = 0; x < width; x++) {
                float confidence = buffer.getFloat();
                int pixel = original.getPixel(x, y);
                
                if (confidence > 0.5f) {
                    result.setPixel(x, y, pixel); // Keep foreground
                } else {
                    result.setPixel(x, y, bgColor); // Apply background
                }
            }
        }
        return result;
    }
}
```

### 14.7 Auto Enhance

#### 14.7.1 Feature Description
Tự động cải thiện chất lượng ảnh (brightness, contrast, saturation, sharpness).

#### 14.7.2 Enhancement Options
```
┌─────────────────────────────────────────────────────┐
│              Auto Enhance                            │
├─────────────────────────────────────────────────────┤
│                                                     │
│  ✨ Smart Enhance (AI)              [ Apply ]      │
│     Automatically adjust all settings               │
│                                                     │
├─────────────────────────────────────────────────────┤
│  Manual Adjustments:                                │
│                                                     │
│  ☀️ Brightness     ○────────●────────○            │
│  🔲 Contrast       ○──────●──────────○            │
│  🎨 Saturation     ○────────────●────○            │
│  🔍 Sharpness      ○────●────────────○            │
│  🌡️ Temperature    ○──────────●──────○            │
│                                                     │
├─────────────────────────────────────────────────────┤
│        [ Reset ]            [ Apply ]               │
└─────────────────────────────────────────────────────┘
```

### 14.8 Scene Detection

#### 14.8.1 Categories
| Category | Icon | Examples |
|----------|------|----------|
| Beach | 🏖️ | Ocean, sand, palm trees |
| Mountain | ⛰️ | Hills, hiking, snow |
| City | 🏙️ | Buildings, streets, urban |
| Nature | 🌿 | Forest, flowers, wildlife |
| Food | 🍕 | Restaurant, cooking |
| People | 👥 | Portrait, group, selfie |
| Pet | 🐕 | Dog, cat, animals |
| Night | 🌙 | Dark, lights, stars |
| Document | 📄 | Text, screenshot |
| Art | 🎨 | Painting, drawing |

#### 14.8.2 Auto-organize by Scene
```
┌─────────────────────────────────────────────────────┐
│               Auto Albums                            │
├─────────────────────────────────────────────────────┤
│  These albums are created automatically by AI       │
├─────────────────────────────────────────────────────┤
│ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐    │
│ │ 🏖️ Beach   │ │ 🍕 Food    │ │ 👥 People   │    │
│ │  45 photos  │ │  89 photos  │ │ 234 photos  │    │
│ └─────────────┘ └─────────────┘ └─────────────┘    │
│ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐    │
│ │ 🐕 Pets    │ │ 📄 Docs    │ │ 🌙 Night    │    │
│ │  23 photos  │ │  67 photos  │ │  34 photos  │    │
│ └─────────────┘ └─────────────┘ └─────────────┘    │
└─────────────────────────────────────────────────────┘
```

---

## 15. Cơ sở dữ liệu

### 15.1 Room Database Schema

#### 15.1.1 Entity: Photo
```java
@Entity(tableName = "photos")
public class PhotoEntity {
    @PrimaryKey
    public long id;                    // MediaStore ID
    
    @ColumnInfo(name = "name")
    public String name;
    
    @ColumnInfo(name = "path")
    public String path;
    
    @ColumnInfo(name = "date_added")
    public long dateAdded;
    
    @ColumnInfo(name = "size")
    public long size;
    
    @ColumnInfo(name = "width")
    public int width;
    
    @ColumnInfo(name = "height")
    public int height;
    
    @ColumnInfo(name = "is_favorite")
    public boolean isFavorite;
    
    @ColumnInfo(name = "is_hidden")
    public boolean isHidden;
    
    @ColumnInfo(name = "is_trashed")
    public boolean isTrashed;
    
    @ColumnInfo(name = "trashed_date")
    public Long trashedDate;
    
    @ColumnInfo(name = "tags")
    public String tags;                // JSON array
    
    @ColumnInfo(name = "detected_faces")
    public String detectedFaces;       // JSON array of face IDs
    
    @ColumnInfo(name = "scene_type")
    public String sceneType;
    
    @ColumnInfo(name = "ocr_text")
    public String ocrText;
}
```

#### 15.1.2 Entity: Album
```java
@Entity(tableName = "albums")
public class AlbumEntity {
    @PrimaryKey(autoGenerate = true)
    public long id;
    
    @ColumnInfo(name = "name")
    public String name;
    
    @ColumnInfo(name = "cover_photo_id")
    public Long coverPhotoId;
    
    @ColumnInfo(name = "is_system")
    public boolean isSystem;           // Favorites, Trash, Hidden
    
    @ColumnInfo(name = "created_date")
    public long createdDate;
    
    @ColumnInfo(name = "photo_count")
    public int photoCount;
}
```

#### 15.1.3 Entity: PhotoAlbum (Junction)
```java
@Entity(
    tableName = "photo_album",
    primaryKeys = {"photo_id", "album_id"},
    foreignKeys = {
        @ForeignKey(entity = PhotoEntity.class, parentColumns = "id", childColumns = "photo_id"),
        @ForeignKey(entity = AlbumEntity.class, parentColumns = "id", childColumns = "album_id")
    }
)
public class PhotoAlbumEntity {
    @ColumnInfo(name = "photo_id")
    public long photoId;
    
    @ColumnInfo(name = "album_id")
    public long albumId;
    
    @ColumnInfo(name = "added_date")
    public long addedDate;
}
```

#### 15.1.4 Entity: Person (for Face Recognition)
```java
@Entity(tableName = "persons")
public class PersonEntity {
    @PrimaryKey(autoGenerate = true)
    public long id;
    
    @ColumnInfo(name = "name")
    public String name;
    
    @ColumnInfo(name = "face_embedding")
    public byte[] faceEmbedding;       // Face feature vector
    
    @ColumnInfo(name = "photo_count")
    public int photoCount;
    
    @ColumnInfo(name = "created_date")
    public long createdDate;
}
```

### 15.2 DAO Interfaces

```java
@Dao
public interface PhotoDao {
    @Query("SELECT * FROM photos WHERE is_trashed = 0 AND is_hidden = 0 ORDER BY date_added DESC")
    LiveData<List<PhotoEntity>> getAllPhotos();
    
    @Query("SELECT * FROM photos WHERE is_favorite = 1 ORDER BY date_added DESC")
    LiveData<List<PhotoEntity>> getFavorites();
    
    @Query("SELECT * FROM photos WHERE is_trashed = 1 ORDER BY trashed_date DESC")
    LiveData<List<PhotoEntity>> getTrashedPhotos();
    
    @Query("SELECT * FROM photos WHERE is_hidden = 1 ORDER BY date_added DESC")
    LiveData<List<PhotoEntity>> getHiddenPhotos();
    
    @Query("SELECT * FROM photos WHERE tags LIKE '%' || :tag || '%'")
    LiveData<List<PhotoEntity>> searchByTag(String tag);
    
    @Query("SELECT * FROM photos WHERE ocr_text LIKE '%' || :text || '%'")
    LiveData<List<PhotoEntity>> searchByText(String text);
    
    @Insert(onConflict = OnConflictStrategy.REPLACE)
    void insert(PhotoEntity photo);
    
    @Update
    void update(PhotoEntity photo);
    
    @Delete
    void delete(PhotoEntity photo);
    
    @Query("UPDATE photos SET is_favorite = :isFavorite WHERE id = :photoId")
    void setFavorite(long photoId, boolean isFavorite);
    
    @Query("UPDATE photos SET is_trashed = 1, trashed_date = :trashedDate WHERE id = :photoId")
    void moveToTrash(long photoId, long trashedDate);
    
    @Query("DELETE FROM photos WHERE is_trashed = 1 AND trashed_date < :threshold")
    void deleteOldTrash(long threshold);
}

@Dao
public interface AlbumDao {
    @Query("SELECT * FROM albums ORDER BY created_date DESC")
    LiveData<List<AlbumEntity>> getAllAlbums();
    
    @Query("SELECT * FROM albums WHERE is_system = 0 ORDER BY name ASC")
    LiveData<List<AlbumEntity>> getUserAlbums();
    
    @Insert
    long insert(AlbumEntity album);
    
    @Update
    void update(AlbumEntity album);
    
    @Delete
    void delete(AlbumEntity album);
}
```

---

## 16. Cấu trúc dự án

```
app/
├── src/main/
│   ├── java/com/example/photoalbum/
│   │   ├── MainActivity.java
│   │   │
│   │   ├── ui/
│   │   │   ├── photos/
│   │   │   │   ├── PhotosFragment.java
│   │   │   │   └── PhotosViewModel.java
│   │   │   ├── albums/
│   │   │   │   ├── AlbumsFragment.java
│   │   │   │   ├── AlbumDetailActivity.java
│   │   │   │   └── AlbumsViewModel.java
│   │   │   ├── favorites/
│   │   │   │   └── FavoritesFragment.java
│   │   │   ├── viewer/
│   │   │   │   ├── PhotoViewerActivity.java
│   │   │   │   └── PhotoPagerAdapter.java
│   │   │   ├── editor/
│   │   │   │   ├── PhotoEditorActivity.java
│   │   │   │   ├── tools/
│   │   │   │   │   ├── RotateTool.java
│   │   │   │   │   ├── FilterTool.java
│   │   │   │   │   ├── BrushTool.java
│   │   │   │   │   └── CropTool.java
│   │   │   │   └── filters/
│   │   │   │       └── PhotoFilters.java
│   │   │   ├── hidden/
│   │   │   │   ├── HiddenPhotosActivity.java
│   │   │   │   └── PasswordActivity.java
│   │   │   ├── trash/
│   │   │   │   └── TrashFragment.java
│   │   │   ├── slideshow/
│   │   │   │   └── SlideshowActivity.java
│   │   │   ├── settings/
│   │   │   │   └── SettingsActivity.java
│   │   │   └── ai/
│   │   │       └── AIFeaturesFragment.java
│   │   │
│   │   ├── adapter/
│   │   │   ├── PhotoAdapter.java
│   │   │   ├── AlbumAdapter.java
│   │   │   └── FilterAdapter.java
│   │   │
│   │   ├── model/
│   │   │   ├── Photo.java
│   │   │   ├── Album.java
│   │   │   └── Person.java
│   │   │
│   │   ├── data/
│   │   │   ├── database/
│   │   │   │   ├── AppDatabase.java
│   │   │   │   ├── PhotoDao.java
│   │   │   │   ├── AlbumDao.java
│   │   │   │   └── PersonDao.java
│   │   │   ├── repository/
│   │   │   │   ├── PhotoRepository.java
│   │   │   │   └── AlbumRepository.java
│   │   │   └── preferences/
│   │   │       └── PreferencesManager.java
│   │   │
│   │   ├── ai/
│   │   │   ├── ImageTagger.java
│   │   │   ├── FaceDetector.java
│   │   │   ├── TextRecognizer.java
│   │   │   ├── BackgroundRemover.java
│   │   │   └── SceneClassifier.java
│   │   │
│   │   └── utils/
│   │       ├── ImageUtils.java
│   │       ├── FileUtils.java
│   │       ├── ShareUtils.java
│   │       ├── PasswordUtils.java
│   │       ├── NetworkUtils.java
│   │       └── ThemeManager.java
│   │
│   └── res/
│       ├── layout/
│       │   ├── activity_main.xml
│       │   ├── activity_photo_viewer.xml
│       │   ├── activity_photo_editor.xml
│       │   ├── activity_album_detail.xml
│       │   ├── activity_slideshow.xml
│       │   ├── activity_password.xml
│       │   ├── fragment_photos.xml
│       │   ├── fragment_albums.xml
│       │   ├── fragment_favorites.xml
│       │   ├── fragment_ai.xml
│       │   ├── item_photo_grid.xml
│       │   ├── item_photo_list.xml
│       │   ├── item_album.xml
│       │   ├── item_filter.xml
│       │   └── item_person.xml
│       │
│       ├── drawable/
│       ├── values/
│       ├── values-night/
│       ├── menu/
│       └── xml/
│
├── build.gradle.kts
└── proguard-rules.pro
```

---

## 17. Yêu cầu kỹ thuật

### 17.1 Dependencies

```kotlin
// build.gradle.kts (app)
dependencies {
    // AndroidX
    implementation("androidx.appcompat:appcompat:1.7.1")
    implementation("com.google.android.material:material:1.13.0")
    implementation("androidx.constraintlayout:constraintlayout:2.2.1")
    implementation("androidx.activity:activity:1.12.2")
    implementation("androidx.fragment:fragment:1.8.6")
    
    // Lifecycle & ViewModel
    implementation("androidx.lifecycle:lifecycle-viewmodel:2.8.8")
    implementation("androidx.lifecycle:lifecycle-livedata:2.8.8")
    
    // Room Database
    implementation("androidx.room:room-runtime:2.6.1")
    annotationProcessor("androidx.room:room-compiler:2.6.1")
    
    // WorkManager (for trash cleanup)
    implementation("androidx.work:work-runtime:2.10.0")
    
    // Image Loading
    implementation("com.github.bumptech.glide:glide:4.16.0")
    
    // PhotoView (for zoom)
    implementation("com.github.chrisbanes:PhotoView:2.3.0")
    
    // ML Kit
    implementation("com.google.mlkit:image-labeling:17.0.7")
    implementation("com.google.mlkit:face-detection:16.1.5")
    implementation("com.google.mlkit:text-recognition:16.0.0")
    implementation("com.google.mlkit:segmentation-selfie:16.0.0-beta4")
    
    // Security
    implementation("androidx.security:security-crypto:1.1.0-alpha06")
    
    // ViewPager2
    implementation("androidx.viewpager2:viewpager2:1.1.0")
}
```

### 17.2 Permissions

```xml
<!-- AndroidManifest.xml -->
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" 
    android:maxSdkVersion="32" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" 
    android:maxSdkVersion="32" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.SET_WALLPAPER" />

<uses-feature android:name="android.hardware.camera" android:required="false" />
```

### 17.3 Min SDK & Target SDK

| Property | Value |
|----------|-------|
| minSdk | 26 (Android 8.0) |
| targetSdk | 34 (Android 14) |
| compileSdk | 34 |

### 17.4 ProGuard Rules

```proguard
# Glide
-keep public class * implements com.bumptech.glide.module.GlideModule
-keep class * extends com.bumptech.glide.module.AppGlideModule

# Room
-keep class * extends androidx.room.RoomDatabase

# ML Kit
-keep class com.google.mlkit.** { *; }
```

---

## 📝 Notes for Development Team

### Priority Order (Sprint Planning)

| Sprint | Features | Priority |
|--------|----------|----------|
| 1 | Photos Gallery, Grid/List View, Sort | P0 - Critical |
| 2 | Photo Viewer, Zoom, Swipe | P0 - Critical |
| 3 | Albums, Create/Delete Album | P1 - High |
| 4 | Favorites, Trash | P1 - High |
| 5 | Photo Editor (Rotate, Crop) | P1 - High |
| 6 | Photo Editor (Filters, Brush) | P2 - Medium |
| 7 | Hidden Photos, Password | P2 - Medium |
| 8 | Slideshow | P2 - Medium |
| 9 | Share, Wallpaper | P2 - Medium |
| 10 | AI Features | P3 - Low |

### Code Style Guidelines
- Sử dụng MVVM architecture
- Đặt tên theo camelCase (Java convention)
- Comment bằng tiếng Anh
- Unit test cho business logic
- UI test cho critical flows

### Git Workflow
```
main
  └── develop
        ├── feature/photos-gallery
        ├── feature/photo-viewer
        ├── feature/albums
        ├── feature/editor
        └── feature/ai-tagging
```

---

*Document Version: 1.0*  
*Created: January 26, 2026*  
*Author: Development Team*
