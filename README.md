# 📊 Global Superstore Sales Analysis — Power BI Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?logo=powerbi&logoColor=black)
![Data Analytics](https://img.shields.io/badge/Data-Analytics-blue)
![DAX](https://img.shields.io/badge/DAX-Measures-green)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

Ushbu loyiha **Global Superstore** (2012–2015) savdo ma'lumotlari asosida **Microsoft Power BI Desktop** dasturida qurilgan interaktiv tahliliy dashboard va ma'lumotlar modelini o'z ichiga oladi. Loyihaning asosiy maqsadi — rahbariyatga savdo hajmi, foyda, buyurtmalar, yetkazib berish muddati va qaytarishlar bo'yicha tezkor va dalillarga asoslangan qaror qabul qilishda yordam berishdir.

---

## 🎯 Loyiha Maqsadi va Vazifalari

* Excel manbalarini Power BI'ga yuklash, ma'lumot turlarini standartlashtirish va tozalash.
* Jadvallar orasidagi bog'lanishlarni (Data Model) to'g'ri o'rnatish hamda takrorlanishlar (`many-to-many`) natijasida KPI ko'rsatkichlari buzilmasligini ta'minlash.
* Asosiy biznes ko'rsatkichlarini hisoblovchi **DAX measure**'larni yaratish.
* 16:9 formatdagi interaktiv **Overview** dashboard sahifasini ishlab chiqish.
* Tahlil natijalari asosida raqamlar bilan tasdiqlangan biznes xulosalarini taqdim etish.

---

## 📁 Ma'lumotlar Manbasi va Model Arxitekturasi

* **Manba fayl:** `global_superstore_2016.xlsx`
* **Vaqt oralig'i:** `2012-01-01` dan `2015-12-31` gacha (4 yil)

### Jadvallar tarkibi:
1. **`Orders` (Buyurtma qatorlari):**
   * **51,290 ta** qator va **25,728 ta** noyob buyurtma (`Order ID`).
   * Bitta buyurtma bir nechta mahsulot qatoriga ega bo'lishi mumkin.
   * Xalqaro buyurtmalarda `Postal Code` bo'sh bo'lgan qatorlar tabiiy holatda saqlangan (sun'iy to'ldirilmagan).
2. **`Returns` (Qaytarilgan buyurtmalar):**
   * **1,079 ta** noyob qaytarilgan `Order ID`.
   * *Model yechimi:* `Sales` va `Profit` summalari ko'payib ketmasligi uchun `Order ID` darajasida Bridge/Dimension jadvali va `DISTINCTCOUNT` yordamida bog'langan.
3. **`People` (Hududiy menejerlar):**
   * **24 ta** noyob `Region` mavjud bo'lib, shundan **22 tasi** `Orders` jadvalidagi hududlar bilan mos keladi (mos kelmagan hududlar savdo hajmi yo'qolmasligi uchun alohida nazoratga olingan).

---

## 🧮 Asosiy KPI va DAX O'lchovlari (Measures)

Modelni tekshirish uchun baza orientirlari va DAX mantiqi:

| Ko'rsatkich (KPI) | DAX Yo'nalishi / Formula Mantiqi | Boshlang'ich Orientir |
| :--- | :--- | :--- |
| **Jami Savdo (Total Sales)** | `SUM(Orders[Sales])` | ~ **$12.64 mln** |
| **Jami Foyda (Total Profit)** | `SUM(Orders[Profit])` *(zararli buyurtmalar bilan)* | ~ **$1.47 mln** |
| **Buyurtmalar Soni (Total Orders)** | `DISTINCTCOUNT(Orders[Order ID])` | **25,728 ta** |
| **Qaytarilgan Buyurtmalar (Returned Orders)** | `DISTINCTCOUNT(Returns[Order ID])` | **1,079 ta** |
| **Qaytarish Darajasi (Return Rate)** | `DIVIDE([Returned Orders], [Total Orders], 0)` | **~ 4.19%** |
| **O'rtacha Yetkazish Kuni (Avg Delivery Days)** | Buyurtma darajasida `Ship Date - Order Date` o'rtachasi | *1 kasr aniqligida* |
| **Foyda Marjasi (Profit Margin %)** | `DIVIDE([Total Profit], [Total Sales], 0)` | **~ 11.63%** |

---

## 📈 Dashboard Tarkibi va Vizualizatsiyalar

Hisobot bitta **Overview (16:9)** sahifasidan iborat bo'lib, quyidagi tahliliy bloklarni qamrab oladi:

1. **KPI Kartalari:** Jami savdo, Jami foyda, Buyurtmalar soni, O'rtacha yetkazish kuni va Qaytarish darajasi.
2. **Vaqt Tahlili (Time Series):** `Order Date` bo'yicha oy va yil kesimida `Sales` hamda `Profit` dinamikasi.
3. **Mahsulotlar Tahlili:** Savdo (`Sales`) bo'yicha **Top 5** va **Bottom 5** mahsulotlar hamda zararli mahsulotlarning `Profit` tahlili.
4. **Mijozlar Tahlili:** Foyda (`Profit`) bo'yicha **Top 10 Customer Name** reytingi.
5. **Segment Tahlili:** Mijoz segmentlari (`Consumer`, `Corporate`, `Home Office`) kesimida savdo va foyda taqqoslamasi.
6. **Geografik Tahlil (Xarita):** Mamlakat va hududlar (`Country/Region`) bo'yicha savdo hajmi.
7. **Logistika va Qaytarishlar:** `Ship Mode` bo'yicha o'rtacha yetkazish kunlari hamda `Region`/`Category` kesimida qaytarish darajasi (`Return Rate`).

### 🎛 Interaktiv Filtrlar (Slicers):
* `Order Date` (Yil yoki sana oralig'i)
* `Region` (Hudud)
* `Category` (Mahsulot toifasi)
* `Segment` (Mijoz segmenti)

---

## 💡 Asosiy Biznes Xulosalari (Insights)

*(Hisobotdagi tahlillar asosida aniqlangan 3 ta asosiy yo'nalish)*:
1. **Vaqt va Mavsumiylik Trendi:** 2012–2015 yillar oralig'ida savdo va foyda bo'yicha eng yuqori o'sish ko'rsatkichlari qayd etilgan yil/oylar tahlili.
2. **Mahsulot va Segment Rentabelligi:** Eng yuqori daromad keltiruvchi Top 5 mahsulot va eng ko'p zarar keltirayotgan (Bottom 5) mahsulotlar hamda yetakchi mijoz segmenti.
3. **Logistika va Qaytarish Muammolari:** Yetkazib berish muddati (`Delivery Days`) va qaytarish darajasi (`Return Rate`) eng yuqori bo'lgan hudud hamda toifalar tahlili.

---

## 🗂 Repozitoriy Tuzilmasi

```text
├── data/
│   └── global_superstore_2016.xlsx      # Manba ma'lumotlar to'plami (Orders, Returns, People)
├── dashboard/
│   ├── Global_Superstore_Report.pbix    # Tayyor Power BI ma'lumotlar modeli va dashboard
│   └── Overview_Screenshot.png          # Dashboard umumiy ko'rinishi (skrinshot)
├── docs/
│   ├── Global_Superstore_Power_BI_TZ.pdf # Loyiha texnik topshirig'i
│   └── Business_Insights.pdf            # 3 ta asosiy biznes xulosasi va KPI ta'riflari
└── README.md                            # Loyiha tavsifi
