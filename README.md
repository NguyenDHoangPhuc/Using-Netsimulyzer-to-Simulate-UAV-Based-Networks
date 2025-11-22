# UAV-Based Network Simulation with NetSimulyzer

## 📋 Mô tả dự án

Dự án này sử dụng **NetSimulyzer** kết hợp với **ns-3** để mô phỏng mạng UAV (Unmanned Aerial Vehicle) trong các kịch bản tìm kiếm và cứu hộ. Đồ án tập trung vào việc nghiên cứu và đánh giá hiệu năng của mạng MANET (Mobile Ad-hoc Network) áp dụng cho UAV-based network.

### 🎯 Mục tiêu

- Xây dựng môi trường mô phỏng mạng UAV hoàn chỉnh
- Đánh giá hiệu năng mạng với giao thức định tuyến AODV
- Trực quan hóa 3D các kịch bản mô phỏng
- Phân tích các yếu tố ảnh hưởng đến hiệu năng mạng

## ✨ Tính năng chính

- 🚁 Mô phỏng mạng UAV với số lượng drone linh hoạt
- 🗺️ Tùy chỉnh kích thước không gian mô phỏng
- 📡 Điều chỉnh công suất phát của thiết bị
- 📊 Thu thập và phân tích dữ liệu real-time
- 🎨 Trực quan hóa 3D với NetSimulyzer
- 📈 Biểu đồ và đồ thị theo dõi hiệu năng

## 🛠️ Công nghệ sử dụng

- **ns-3.38**: Network Simulator 3
- **NetSimulyzer 1.0.7**: 3D Visualization Tool
- **AODV Protocol**: Ad-hoc On-demand Distance Vector Routing
- **Ubuntu 22.04**: Operating System
- **C++**: Programming Language
- **Python**: Scripting & Analysis

## 📦 Cài đặt

### 1. Chuẩn bị môi trường
```bash
# Cập nhật hệ thống
sudo apt update

# Cài đặt các thư viện cần thiết
sudo apt install g++ python3 cmake ninja-build git \
  gir1.2-goocanvas-2.0 python3-gi python3-gi-cairo \
  python3-pygraphviz gir1.2-gtk-3.0 ipython3 tcpdump \
  wireshark sqlite sqlite3 libsqlite3-dev qtbase5-dev \
  qtchooser qt5-qmake qtbase5-dev-tools openmpi-bin \
  openmpi-common openmpi-doc libopenmpi-dev doxygen \
  graphviz imagemagick python3-sphinx dia texlive \
  dvipng latexmk texlive-extra-utils texlive-latex-extra \
  texlive-font-utils libeigen3-dev gsl-bin libgsl-dev \
  libgslcblas0 libxml2 libxml2-dev libgtk-3-dev \
  lxc-utils lxc-templates vtun uml-utilities ebtables \
  bridge-utils libboost-all-dev
```

### 2. Cài đặt ns-3
```bash
# Tải ns-3.38
wget https://www.nsnam.org/releases/ns-allinone-3.38.tar.bz2
tar xjf ns-allinone-3.38.tar.bz2
cd ns-allinone-3.38/ns-3.38

# Build ns-3
./build.py --enable-tests --enable-examples

# Test installation
./test.py
```

### 3. Cài đặt NetSimulyzer Module
```bash
# Tải NetSimulyzer module
cd contrib
wget https://github.com/usnistgov/NetSimulyzer-ns3-module/archive/master.zip -O NetSimulyzer-ns3-module.zip
unzip NetSimulyzer-ns3-module.zip
mv NetSimulyzer-ns3-module-master netsimulyzer

# Build lại ns-3
cd ..
./build.py --enable-tests --enable-examples
```

### 4. Cài đặt NetSimulyzer Application
```bash
# Clone repository
git clone --recursive https://github.com/usnistgov/NetSimulyzer.git
cd NetSimulyzer

# Build application
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
cmake --build .

# Chạy NetSimulyzer
./netsimulyzer
```

## 🚀 Sử dụng

### Chạy mô phỏng
```bash
# Copy file mô phỏng vào thư mục scratch
cp your-simulation-file.cc ns-3.38/scratch/

# Chạy mô phỏng
cd ns-3.38
./ns3 run scratch/your-simulation-file

# File JSON output sẽ được tạo trong thư mục hiện tại
```

### Trực quan hóa với NetSimulyzer
```bash
# Mở NetSimulyzer
cd NetSimulyzer/build
./netsimulyzer

# Load file JSON từ menu File → Open
# Nhấn Play để xem mô phỏng 3D
```

## 📊 Kịch bản mô phỏng

### Kịch bản 1: Thay đổi số lượng UAV

| Thông số | Giá trị |
|----------|---------|
| Số lượng UAV | 10, 25, 50 |
| Tốc độ UAV | 10-20 m/s |
| Kích thước map | 500x500 m |
| Công suất phát | 30 dBm |

**Kết quả:**
- **10 UAV**: Thời gian phát hiện chậm (108.1s), mất gói tin
- **25 UAV**: Hiệu quả tối ưu, không mất gói tin (24.1s)
- **50 UAV**: Phát hiện nhanh nhất (0.1s), chi phí cao

### Kịch bản 2: Thay đổi kích thước map

| Thông số | Giá trị |
|----------|---------|
| Số lượng UAV | 100 |
| Tốc độ UAV | 10-20 m/s |
| Kích thước map | 1250x1250, 1500x1500, 2000x2000 m |
| Công suất phát | 40 dBm |

**Kết quả:**
- **1250x1250m**: Hiệu quả cao, phát hiện nhanh (12.1s)
- **1500x1500m**: Hiệu quả tốt, phát hiện chậm hơn (18.1s)
- **2000x2000m**: Khó khăn trong định tuyến, mất gói tin (81.1s)

### Kịch bản 3: Thay đổi công suất phát

| Thông số | Giá trị |
|----------|---------|
| Số lượng UAV | 25 |
| Tốc độ UAV | 10-20 m/s |
| Kích thước map | 750x750 m |
| Công suất phát | 20, 45, 75 dBm |

**Kết quả:**
- **20 dBm**: Không xây dựng được đường đi, mất tất cả gói tin
- **45 dBm**: Hiệu quả tốt, cân bằng giữa hiệu năng và thực tế
- **75 dBm**: Tốc độ cao nhất, nhưng ít thực tế

## 📈 Các chỉ số đánh giá

- **Throughput**: Thông lượng mạng
- **Delay**: Độ trễ truyền dẫn
- **Jitter**: Độ biến động trễ
- **Packet Loss Rate**: Tỷ lệ mất gói tin
- **Energy Consumption**: Tiêu thụ năng lượng
- **Routing Overhead**: Chi phí định tuyến

## 🔧 Công cụ phân tích

- **FlowMonitor**: Phân tích luồng dữ liệu
- **NetAnim**: Trực quan hóa 2D
- **Wireshark**: Phân tích gói tin chi tiết
- **NetSimulyzer**: Trực quan hóa 3D

## 📁 Cấu trúc dự án
```
project/
├── scratch/
│   └── uav-search-rescue.cc      # File mô phỏng chính
├── contrib/
│   └── netsimulyzer/              # NetSimulyzer module
├── results/
│   ├── *.json                     # File output NetSimulyzer
│   ├── *.xml                      # File output NetAnim
│   └── *.pcap                     # File capture Wireshark
└── docs/
    └── report.pdf                 # Báo cáo đồ án
```

## 🎓 Các thành phần chính của code

### Khai báo biến và cấu hình
```cpp
uint32_t nDrones = 25;           // Số lượng UAV
uint32_t nTargets = 3;           // Số người cần tìm
uint32_t mapSize = 500;          // Kích thước map (m)
double txPower = 30.0;           // Công suất phát (dBm)
double detectionRange = 50.0;    // Tầm phát hiện (m)
```

### Cấu hình WiFi và AODV
```cpp
// Cấu hình WiFi
WifiHelper wifi;
wifi.SetStandard(WIFI_PHY_STANDARD_80211a);

// Cấu hình AODV routing
AodvHelper aodv;
InternetStackHelper stack;
stack.SetRoutingHelper(aodv);
stack.Install(nodes);
```

### Cấu hình di chuyển
```cpp
// Random Waypoint Mobility Model
MobilityHelper mobility;
mobility.SetPositionAllocator("ns3::RandomRectanglePositionAllocator");
mobility.SetMobilityModel("ns3::RandomWaypointMobilityModel",
                          "Speed", StringValue("ns3::UniformRandomVariable[Min=10.0|Max=20.0]"));
mobility.Install(drones);
```

### Thu thập dữ liệu
```cpp
// FlowMonitor
FlowMonitorHelper flowmon;
Ptr<FlowMonitor> monitor = flowmon.InstallAll();

// NetSimulyzer Orchestrator
auto orchestrator = CreateObject<netsimulyzer::Orchestrator>("output.json");
```

## 📊 Kết quả nghiên cứu

### So sánh số lượng UAV

| Số UAV | Thời gian (s) | Gói tin thành công | Chi phí |
|--------|---------------|-------------------|---------|
| 10     | 108.1         | 1/3               | Thấp    |
| 25     | 24.1          | 3/3               | Trung bình |
| 50     | 0.1           | 3/3               | Cao     |

### So sánh kích thước map

| Kích thước | Thời gian (s) | Gói tin thành công |
|------------|---------------|--------------------|
| 1250x1250m | 12.1          | 3/3                |
| 1500x1500m | 18.1          | 3/3                |
| 2000x2000m | 81.1          | 2/3                |

### So sánh công suất phát

| Công suất | Gói tin thành công | Tính thực tế |
|-----------|-------------------|--------------|
| 20 dBm    | 0/3               | Cao          |
| 45 dBm    | 3/3               | Trung bình   |
| 75 dBm    | 3/3               | Thấp         |

## 🔬 Hướng phát triển

- [ ] Tích hợp Reinforcement Learning cho định tuyến thông minh
- [ ] Mở rộng các kịch bản với chướng ngại vật và thời tiết
- [ ] So sánh với các giao thức định tuyến khác (DSR, OLSR)
- [ ] Tích hợp với hardware thực tế
- [ ] Tối ưu hóa tiêu thụ năng lượng

## 👥 Nhóm thực hiện

**Nhóm 1 - NT131.P12**

| Thành viên | MSSV | Vai trò |
|------------|------|---------|
| Nguyễn Dương Hoàng Phúc | 22521125 | Trưởng nhóm |
| Phan Văn Tài | 22521284 | Thành viên |

**Giảng viên hướng dẫn**: ThS. Đặng Lê Bảo Chương

**Trường**: Đại học Công nghệ Thông tin, ĐHQG-HCM

**Thời gian**: 25/10/2024 – 15/12/2024

## 📚 Tài liệu tham khảo

1. [NetSimulyzer GitHub](https://github.com/usnistgov/NetSimulyzer)
2. [ns-3 Documentation](https://www.nsnam.org/)
3. [NetSimulyzer ns-3 Module](https://github.com/usnistgov/NetSimulyzer-ns3-module)
4. [AODV RFC 3561](https://www.ietf.org/rfc/rfc3561.txt)
5. [ns-3 Tutorial](https://www.nsnam.org/docs/tutorial/html/)

## 📄 License

Dự án này được thực hiện cho mục đích học tập và nghiên cứu tại Trường Đại học Công nghệ Thông tin, ĐHQG-HCM.
