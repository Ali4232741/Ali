import pandas as pd

# خواندن فایل CSV
df = pd.read_csv('/content/drive/MyDrive/دیتاست چالش شماره یک کی‌بُرد.csv')

# تعداد مقادیر از دست رفته در کل DataFrame
total_missing = df.isna().sum().sum()

# تعداد مقادیر از دست رفته در هر ستون
missing_per_column = df.isna().sum()

# نمایش نتایج
print(f"تعداد مقادیر از دست رفته در کل DataFrame: {total_missing}")
print("تعداد مقادیر از دست رفته در هر ستون:")
print(missing_per_column)

# جایگزینی مقادیر از دست رفته با میانگین (برای داده‌های عددی)
df.fillna(df.mean(), inplace=True)



# جایگزینی مقادیر از دست رفته با مد (برای داده‌های غیر عددی)
for column in df.select_dtypes(include=['object']).columns:
    df[column].fillna(df[column].mode()[0], inplace=True)

# محاسبه و نمایش تعداد مقادیر از دست رفته پس از جایگزینی
total_missing_after = df.isna().sum().sum()
missing_per_column_after = df.isna().sum()

print(f"تعداد مقادیر از دست رفته در کل DataFrame پس از جایگزینی: {total_missing_after}")
print("تعداد مقادیر از دست رفته در هر ستون پس از جایگزینی:")
print(missing_per_column_after)
