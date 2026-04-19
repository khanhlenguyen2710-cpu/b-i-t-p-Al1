# b-i-t-p-Al1
import folium

# 1. Khởi tạo bản đồ với tọa độ trung tâm là UEH - Cơ sở A (59C Nguyễn Đình Chiểu, Quận 3)
# Tọa độ xấp xỉ: 10.7828, 106.6958
ueh_coords = [10.7828, 106.6958]
m = folium.Map(location=ueh_coords, zoom_start=16)

# 2. Tạo các nhóm lớp (Feature Groups) để có thể bật/tắt
fg_ueh = folium.FeatureGroup(name='Trường Đại học')
fg_public = folium.FeatureGroup(name='Địa điểm công cộng lân cận')

# 3. Thêm marker cho UEH
folium.Marker(
    location=ueh_coords,
    popup='Đại học Kinh tế TP.HCM (UEH) - Cơ sở A',
    icon=folium.Icon(color='red', icon='graduation-cap', prefix='fa')
).add_to(fg_ueh)

# 4. Danh sách 5 địa điểm công cộng lân cận
locations = [
    {"name": "Hồ Con Rùa", "coord": [10.7825, 106.6961], "info": "Địa điểm vui chơi công cộng"},
    {"name": "Nhà Văn hóa Thanh Niên", "coord": [10.7820, 106.6975], "info": "Trung tâm hoạt động thanh niên"},
    {"name": "Bệnh viện Da Liễu TP.HCM", "coord": [10.7850, 106.6915], "info": "Cơ sở y tế chuyên khoa"},
    {"name": "Diamond Plaza", "coord": [10.7802, 106.6988], "info": "Trung tâm thương mại lớn"},
    {"name": "Bưu điện Trung tâm Thành phố", "coord": [10.7798, 106.6999], "info": "Cơ quan hành chính/Tham quan"}
]

# Thêm các marker địa điểm công cộng vào FeatureGroup
for loc in locations:
    folium.Marker(
        location=loc["coord"],
        popup=f"<b>{loc['name']}</b>: {loc['info']}",
        icon=folium.Icon(color='blue', icon='info-sign')
    ).add_to(fg_public)

# 5. Thêm các lớp vào bản đồ và tạo bảng điều khiển lớp (Layer Control)
fg_ueh.add_to(m)
fg_public.add_to(m)
folium.LayerControl().add_to(m)

# 6. Lưu bản đồ thành file HTML để xem
m.save("ban_do_tuong_tac_ueh.html")
print("Đã tạo bản đồ thành công! Hãy mở file 'ban_do_tuong_tac_ueh.html' để xem kết quả.")
