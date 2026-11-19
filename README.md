# 12A3-Tin
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Ôn Tập Tin Học 12 - Nút Bấm Dễ Chạm</title>
  <style>
    * {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }
    body {
      font-family: Arial, sans-serif;
      background: #f1f5f9;
      color: #0f172a;
      margin: 0;
      padding: 12px;
      line-height: 1.5;
    }
    .container {
      max-width: 820px;
      margin: 0 auto;
      background: #ffffff;
      padding: 18px;
      border-radius: 16px;
      box-shadow: 0 6px 20px rgba(15, 23, 42, 0.08);
    }
    h1 {
      margin: 0 0 8px 0;
      font-size: 20px;
      color: #1d4ed8;
    }
    .info {
      background: #eff6ff;
      border-left: 4px solid #2563eb;
      padding: 12px;
      border-radius: 10px;
      margin-bottom: 14px;
      font-size: 14px;
    }
    .progress-bar {
      position: sticky;
      top: 8px;
      z-index: 10;
      background: rgba(255, 255, 255, 0.96);
      border: 1px solid #cbd5e1;
      border-radius: 12px;
      padding: 10px 14px;
      margin-bottom: 16px;
      font-size: 14px;
      font-weight: bold;
      color: #1e3a8a;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
    }
    .question-card {
      border: 1px solid #e2e8f0;
      border-radius: 14px;
      padding: 14px;
      margin-bottom: 16px;
      background: #f8fafc;
    }
    .q-title {
      font-weight: bold;
      font-size: 15.5px;
      margin-bottom: 12px;
    }
    .badge {
      display: inline-block;
      font-size: 12px;
      padding: 3px 9px;
      border-radius: 999px;
      background: #dbeafe;
      color: #1e40af;
      margin-right: 4px;
      margin-bottom: 4px;
      font-weight: bold;
    }
    /* Nút đáp án A, B, C, D lớn dễ bấm */
    .choice-btn {
      width: 100%;
      min-height: 50px;
      display: flex;
      align-items: center;
      gap: 10px;
      text-align: left;
      padding: 10px 14px;
      margin: 8px 0;
      background: #ffffff;
      color: #0f172a;
      border: 2px solid #cbd5e1;
      border-radius: 12px;
      font-size: 15px;
      cursor: pointer;
      transition: all 0.15s ease;
    }
    .choice-btn:active {
      transform: scale(0.99);
    }
    .choice-btn.selected {
      background: #dbeafe;
      border-color: #2563eb;
      color: #1e3a8a;
      font-weight: bold;
    }
    .choice-key {
      min-width: 28px;
      height: 28px;
      border-radius: 8px;
      background: #e2e8f0;
      color: #0f172a;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
      flex-shrink: 0;
    }
    .choice-btn.selected .choice-key {
      background: #2563eb;
      color: #ffffff;
    }

    /* Khối Đúng / Sai dạng nút bấm lớn */
    .tf-box {
      background: #ffffff;
      border: 1px solid #e2e8f0;
      border-radius: 12px;
      padding: 12px;
      margin: 10px 0;
    }
    .tf-text {
      font-size: 15px;
      margin-bottom: 10px;
    }
    .tf-btn-group {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }
    .tf-btn {
      min-height: 46px;
      border-radius: 10px;
      border: 2px solid #cbd5e1;
      background: #f8fafc;
      color: #0f172a;
      font-size: 15px;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.15s ease;
    }
    .tf-btn:active {
      transform: scale(0.98);
    }
    .tf-btn.selected-true {
      background: #dcfce7;
      border-color: #16a34a;
      color: #166534;
    }
    .tf-btn.selected-false {
      background: #fee2e2;
      border-color: #dc2626;
      color: #991b1b;
    }

    .actions {
      display: grid;
      grid-template-columns: 1fr;
      gap: 12px;
      margin-top: 20px;
    }
    @media (min-width: 600px) {
      .actions {
        grid-template-columns: 2fr 1fr;
      }
    }
    .action-btn {
      min-height: 52px;
      padding: 12px 20px;
      font-size: 16px;
      font-weight: bold;
      border: none;
      border-radius: 12px;
      cursor: pointer;
    }
    .btn-submit {
      background: #16a34a;
      color: #ffffff;
    }
    .btn-reset {
      background: #e2e8f0;
      color: #0f172a;
    }
    #result-box {
      margin-top: 20px;
      padding: 16px;
      border-radius: 12px;
      background: #ecfdf5;
      border: 2px solid #34d399;
      font-size: 15.5px;
      display: none;
    }
    .explain {
      margin-top: 12px;
      padding: 12px;
      background: #fefce8;
      border-left: 4px solid #eab308;
      border-radius: 10px;
      font-size: 14px;
      display: none;
    }
    .correct-text { color: #15803d; font-weight: bold; }
    .wrong-text { color: #b91c1c; font-weight: bold; }
  </style>
</head>
<body>
  <div class="container">
    <h1>Ôn Tập Tin Học 12 (20 Câu: Trắc Nghiệm &amp; Đúng/Sai)</h1>
    <div class="info">
      Chủ đề: <strong>Mạng máy tính</strong> &amp; <strong>Cơ sở dữ liệu</strong>. Chạm trực tiếp vào từng nút đáp án để chọn.
    </div>

    <div class="progress-bar">
      <span id="progress-text">Đã làm: 0 / 20 câu</span>
      <span>Chế độ chạm điện thoại</span>
    </div>

    <div id="quiz-container"></div>

    <div class="actions">
      <button type="button" class="action-btn btn-submit" onclick="gradeQuiz()">Nộp bài &amp; Xem điểm</button>
      <button type="button" class="action-btn btn-reset" onclick="resetQuiz()">Làm lại từ đầu</button>
    </div>

    <div id="result-box"></div>
  </div>

  <script>
    const questions = [
      // --- TRẮC NGHIỆM 4 LỰA CHỌN (Câu 1 - Câu 14) ---
      {
        id: 1, type: "mcq", topic: "Mạng máy tính",
        q: "Thiết bị nào hoạt động ở tầng mạng (Network Layer) và dùng để kết nối các mạng khác nhau?",
        options: { A: "Hub", B: "Switch", C: "Router", D: "Repeater" },
        ans: "C",
        explain: "Router (bộ định tuyến) dẫn đường gói tin giữa các mạng khác nhau dựa trên địa chỉ IP."
      },
      {
        id: 2, type: "mcq", topic: "Mạng máy tính",
        q: "Giao thức nào chịu trách nhiệm phân giải tên miền (như google.com) thành địa chỉ IP?",
        options: { A: "HTTP", B: "DNS", C: "FTP", D: "SMTP" },
        ans: "B",
        explain: "DNS (Domain Name System) dịch tên miền dễ nhớ sang địa chỉ IP để máy tính định vị trên mạng."
      },
      {
        id: 3, type: "mcq", topic: "Mạng máy tính",
        q: "Điểm khác biệt cơ bản của HTTPS so với HTTP là gì?",
        options: {
          A: "Tải ảnh nhanh hơn gấp đôi",
          B: "Không cần dùng trình duyệt web",
          C: "Mã hóa dữ liệu truyền tải qua giao thức bảo mật",
          D: "Chỉ dùng cho mạng nội bộ LAN"
        },
        ans: "C",
        explain: "HTTPS mã hóa dữ liệu bằng TLS/SSL, giúp bảo vệ thông tin khi truyền trên mạng."
      },
      {
        id: 4, type: "mcq", topic: "Mạng máy tính",
        q: "Địa chỉ IPv4 có độ dài bao nhiêu bit?",
        options: { A: "16 bit", B: "32 bit", C: "64 bit", D: "128 bit" },
        ans: "B",
        explain: "Địa chỉ IPv4 gồm 32 bit, thường viết dưới dạng 4 số thập phân cách nhau bởi dấu chấm."
      },
      {
        id: 5, type: "mcq", topic: "Mạng máy tính",
        q: "Chức năng chính của tường lửa (Firewall) trong bảo mật mạng là gì?",
        options: {
          A: "Tăng dung lượng ổ cứng máy chủ",
          B: "Kiểm soát và lọc lưu lượng mạng ra vào theo quy tắc bảo mật",
          C: "Tự động dịch ngôn ngữ trang web",
          D: "Thay thế hoàn toàn phần mềm diệt virus"
        },
        ans: "B",
        explain: "Firewall giám sát và chặn/cho phép các kết nối mạng dựa trên tập luật an toàn thông tin."
      },
      {
        id: 6, type: "mcq", topic: "Mạng máy tính",
        q: "Mạng LAN thường có phạm vi hoạt động như thế nào?",
        options: {
          A: "Trong một gia đình, phòng học, tòa nhà hoặc cơ quan",
          B: "Xuyên suốt các châu lục qua vệ tinh",
          C: "Chỉ kết nối hai điện thoại qua Bluetooth",
          D: "Chỉ dùng cho máy chủ đám mây"
        },
        ans: "A",
        explain: "LAN (Local Area Network) là mạng cục bộ trong phạm vi hẹp như phòng học, trường học, văn phòng."
      },
      {
        id: 7, type: "mcq", topic: "Mạng máy tính",
        q: "Trong mô hình Client - Server, máy Client có vai trò gì?",
        options: {
          A: "Chỉ lưu trữ tệp cấu hình hệ điều hành",
          B: "Gửi yêu cầu dịch vụ và hiển thị kết quả nhận từ Server",
          C: "Quản lý toàn bộ tài khoản người dùng toàn cầu",
          D: "Thay thế bộ phát Wi-Fi"
        },
        ans: "B",
        explain: "Máy khách (Client) gửi yêu cầu tới máy chủ (Server) để nhận dữ liệu hoặc dịch vụ."
      },
      {
        id: 8, type: "mcq", topic: "Cơ sở dữ liệu",
        q: "Cơ sở dữ liệu (CSDL) là gì?",
        options: {
          A: "Một tệp văn bản ghi chép ngẫu nhiên không có cấu trúc",
          B: "Tập hợp dữ liệu có cấu trúc, có liên quan với nhau và được lưu trữ có tổ chức",
          C: "Phần mềm soạn thảo bảng tính",
          D: "Một thiết bị lưu trữ gắn ngoài"
        },
        ans: "B",
        explain: "CSDL lưu trữ dữ liệu có tổ chức, có cấu trúc rõ ràng để nhiều người dùng khai thác hiệu quả."
      },
      {
        id: 9, type: "mcq", topic: "Cơ sở dữ liệu",
        q: "Trong CSDL quan hệ, khóa chính (Primary Key) có đặc điểm nào sau đây?",
        options: {
          A: "Có thể chứa nhiều giá trị trùng nhau",
          B: "Dùng để phân biệt duy nhất mỗi bản ghi (hàng) trong bảng",
          C: "Bắt buộc phải là kiểu văn bản dài",
          D: "Tự động xóa dữ liệu mỗi ngày"
        },
        ans: "B",
        explain: "Khóa chính xác định duy nhất từng bộ/bản ghi trong bảng và không nhận giá trị rỗng (NULL)."
      },
      {
        id: 10, type: "mcq", topic: "Cơ sở dữ liệu",
        q: "Khóa ngoại (Foreign Key) trong CSDL quan hệ dùng để làm gì?",
        options: {
          A: "Mã hóa mật khẩu quản trị viên",
          B: "Liên kết dữ liệu giữa hai bảng và đảm bảo tính toàn vẹn tham chiếu",
          C: "Tăng tốc độ gõ phím",
          D: "Định dạng màu chữ của bảng"
        },
        ans: "B",
        explain: "Khóa ngoại trỏ tới khóa chính của bảng khác nhằm liên kết bảng và giữ tính nhất quán dữ liệu."
      },
      {
        id: 11, type: "mcq", topic: "Cơ sở dữ liệu",
        q: "Câu lệnh SQL nào dùng để truy vấn (lấy) dữ liệu từ bảng?",
        options: { A: "SELECT", B: "DELETE", C: "DROP", D: "ALTER" },
        ans: "A",
        explain: "SELECT dùng để truy xuất dữ liệu từ một hoặc nhiều bảng theo điều kiện."
      },
      {
        id: 12, type: "mcq", topic: "Cơ sở dữ liệu",
        q: "Mệnh đề nào trong câu lệnh SQL dùng để lọc các bản ghi thỏa mãn điều kiện?",
        options: { A: "GROUP BY", B: "ORDER BY", C: "WHERE", D: "VALUES" },
        ans: "C",
        explain: "WHERE quy định điều kiện lọc các dòng dữ liệu trước khi trả về kết quả."
      },
      {
        id: 13, type: "mcq", topic: "Cơ sở dữ liệu",
        q: "Câu lệnh SQL nào dùng để thêm một bản ghi mới vào bảng?",
        options: { A: "UPDATE", B: "INSERT INTO", C: "CREATE TABLE", D: "GRANT" },
        ans: "B",
        explain: "INSERT INTO thêm hàng dữ liệu mới vào bảng chỉ định."
      },
      {
        id: 14, type: "mcq", topic: "Cơ sở dữ liệu",
        q: "Hệ quản trị cơ sở dữ liệu (DBMS) giúp người dùng thực hiện công việc nào?",
        options: {
          A: "Tạo lập, cập nhật, truy vấn và kiểm soát truy cập CSDL",
          B: "Thiết kế mạch điện tử bên trong CPU",
          C: "Thay thế trình duyệt web",
          D: "Nén file âm thanh MP3"
        },
        ans: "A",
        explain: "DBMS (như MySQL) cung cấp công cụ định nghĩa, thao tác, bảo mật và quản trị CSDL."
      },

      // --- TRẮC NGHIỆM ĐÚNG / SAI (Câu 15 - Câu 20) ---
      {
        id: 15, type: "tf", topic: "Mạng máy tính",
        q: "Một học sinh cấu hình mạng không dây và truy cập dịch vụ web. Hãy đánh giá các nhận định sau là Đúng hay Sai:",
        statements: {
          a: { text: "Giao thức HTTP truyền dữ liệu dạng văn bản thuần, dễ bị nghe lén hơn HTTPS.", ans: true },
          b: { text: "Địa chỉ MAC là địa chỉ logic do người dùng tự đổi mọi lúc khi kết nối Wi-Fi.", ans: false },
          c: { text: "Khi bật Chế độ máy bay, thiết bị ngắt các kết nối vô tuyến như di động/Wi-Fi.", ans: true },
          d: { text: "Mọi thiết bị trong cùng mạng LAN đều có cùng địa chỉ IP giống hệt nhau.", ans: false }
        },
        explain: "a) Đúng. b) Sai: địa chỉ MAC gắn với card mạng (cấp phần cứng, không phải địa chỉ IP logic). c) Đúng. d) Sai: mỗi thiết bị trong mạng cần địa chỉ IP riêng để phân biệt."
      },
      {
        id: 16, type: "tf", topic: "Mạng máy tính",
        q: "Khi sử dụng Internet để học tập và chia sẻ tài liệu trực tuyến, các phát biểu sau Đúng hay Sai?",
        statements: {
          a: { text: "Đặt mật khẩu mạnh và bật xác thực hai yếu tố (2FA) giúp giảm rủi ro mất tài khoản.", ans: true },
          b: { text: "Nhấp vào mọi đường link lạ gửi qua tin nhắn để nhận quà là thao tác an toàn.", ans: false },
          c: { text: "Cập nhật bản vá bảo mật thường xuyên giúp khắc phục lỗ hổng phần mềm.", ans: true },
          d: { text: "Chia sẻ công khai mật khẩu cá nhân cho cả nhóm là cách tốt nhất để quản lý.", ans: false }
        },
        explain: "a) Đúng. b) Sai: dễ gặp lừa đảo (phishing) hoặc mã độc. c) Đúng. d) Sai: làm lộ thông tin cá nhân và tăng nguy cơ bị xâm nhập."
      },
      {
        id: 17, type: "tf", topic: "Mạng máy tính",
        q: "Xét các đặc điểm về thiết bị và truyền thông mạng máy tính dưới đây:",
        statements: {
          a: { text: "Access Point giúp các thiết bị không dây kết nối vào mạng có dây/mạng cục bộ.", ans: true },
          b: { text: "Switch chỉ hoạt động trên mạng toàn cầu và không dùng trong mạng LAN.", ans: false },
          c: { text: "Băng thông càng lớn thường giúp truyền tải lượng dữ liệu lớn nhanh hơn.", ans: true },
          d: { text: "Mất kết nối Internet nghĩa là máy tính không thể chạy ứng dụng đã lưu sẵn cục bộ.", ans: false }
        },
        explain: "a) Đúng. b) Sai: Switch dùng phổ biến trong mạng LAN. c) Đúng. d) Sai: ứng dụng/dữ liệu lưu sẵn trên máy hoặc bộ nhớ đệm vẫn có thể chạy ngoại tuyến."
      },
      {
        id: 18, type: "tf", topic: "Cơ sở dữ liệu",
        q: "Trong một cơ sở dữ liệu quản lý học sinh gồm hai bảng HOC_SINH (MaHS, HoTen, MaLop) và LOP (MaLop, TenLop):",
        statements: {
          a: { text: "MaHS có thể chọn làm khóa chính của bảng HOC_SINH để định danh từng học sinh.", ans: true },
          b: { text: "MaLop ở bảng HOC_SINH đóng vai trò khóa ngoại liên kết tới bảng LOP.", ans: true },
          c: { text: "Hai học sinh khác nhau có thể cùng mang một giá trị MaHS nếu cùng lớp.", ans: false },
          d: { text: "Có thể dùng câu lệnh SELECT để lấy danh sách học sinh theo từng lớp.", ans: true }
        },
        explain: "a) Đúng. b) Đúng. c) Sai: khóa chính không được trùng lặp. d) Đúng: SELECT kết hợp điều kiện hoặc JOIN giúp truy vấn thông tin theo lớp."
      },
      {
        id: 19, type: "tf", topic: "Cơ sở dữ liệu",
        q: "Khi cập nhật và bảo vệ dữ liệu trong hệ cơ sở dữ liệu, các nhận định sau Đúng hay Sai?",
        statements: {
          a: { text: "Câu lệnh UPDATE dùng để sửa đổi dữ liệu hiện có trong bảng.", ans: true },
          b: { text: "Câu lệnh DELETE không bao giờ cần mệnh đề WHERE vì luôn xóa toàn bộ bảng.", ans: false },
          c: { text: "Phân quyền người dùng giúp hạn chế người không có thẩm quyền sửa/xóa dữ liệu quan trọng.", ans: true },
          d: { text: "Sao lưu (backup) dữ liệu định kỳ giúp khôi phục khi gặp sự cố hệ thống.", ans: true }
        },
        explain: "a) Đúng. b) Sai: DELETE thường dùng kèm WHERE để xóa đúng bản ghi cần thiết. c) Đúng. d) Đúng."
      },
      {
        id: 20, type: "tf", topic: "Cơ sở dữ liệu",
        q: "So sánh việc lưu dữ liệu bằng CSDL với lưu rời rạc trên nhiều tệp văn bản thông thường:",
        statements: {
          a: { text: "CSDL giảm trùng lặp dữ liệu và tăng tính nhất quán hơn so với lưu rời rạc.", ans: true },
          b: { text: "CSDL hỗ trợ tìm kiếm, lọc và tổng hợp dữ liệu nhanh chóng bằng ngôn ngữ truy vấn.", ans: true },
          c: { text: "Trong CSDL, mọi người dùng đều có toàn quyền xóa dữ liệu của người khác.", ans: false },
          d: { text: "Tổ chức bảng hợp lý giúp dễ dàng mở rộng dữ liệu khi quy mô tăng lên.", ans: true }
        },
        explain: "a) Đúng. b) Đúng. c) Sai: hệ thống phân quyền kiểm soát ai được xem, thêm, sửa, xóa. d) Đúng."
      }
    ];

    const userAnswers = {}; // Lưu lựa chọn: mcq -> "A"/"B"/"C"/"D", tf -> { a: true/false, ... }
    const containerEl = document.getElementById("quiz-container");
    const progressEl = document.getElementById("progress-text");

    function renderQuiz() {
      containerEl.innerHTML = "";
      questions.forEach((item) => {
        const card = document.createElement("div");
        card.className = "question-card";

        const typeLabel = item.type === "mcq" ? "Trắc nghiệm" : "Đúng / Sai";
        let html = `
          <div class="q-title">
            <span class="badge">Câu ${item.id}</span>
            <span class="badge">${item.topic}</span>
            <span class="badge">${typeLabel}</span>
            <div>${item.q}</div>
          </div>
        `;

        if (item.type === "mcq") {
          for (const [key, val] of Object.entries(item.options)) {
            html += `
              <button type="button" class="choice-btn" id="btn_q${item.id}_${key}" onclick="selectMCQ(${item.id}, '${key}')">
                <span class="choice-key">${key}</span>
                <span>${val}</span>
              </button>
            `;
          }
        } else {
          for (const [subKey, subObj] of Object.entries(item.statements)) {
            html += `
              <div class="tf-box">
                <div class="tf-text"><strong>${subKey})</strong> ${subObj.text}</div>
                <div class="tf-btn-group">
                  <button type="button" class="tf-btn" id="btn_q${item.id}_${subKey}_true" onclick="selectTF(${item.id}, '${subKey}', true)">Đúng</button>
                  <button type="button" class="tf-btn" id="btn_q${item.id}_${subKey}_false" onclick="selectTF(${item.id}, '${subKey}', false)">Sai</button>
                </div>
              </div>
            `;
          }
        }

        html += `<div class="explain" id="explain_${item.id}"></div>`;
        card.innerHTML = html;
        containerEl.appendChild(card);
      });
      updateProgress();
    }

    function selectMCQ(qId, choice) {
      userAnswers[qId] = choice;
      ["A", "B", "C", "D"].forEach((k) => {
        const btn = document.getElementById(`btn_q${qId}_${k}`);
        if (btn) btn.classList.toggle("selected", k === choice);
      });
      updateProgress();
    }

    function selectTF(qId, subKey, val) {
      if (!userAnswers[qId]) userAnswers[qId] = {};
      userAnswers[qId][subKey] = val;

      const btnTrue = document.getElementById(`btn_q${qId}_${subKey}_true`);
      const btnFalse = document.getElementById(`btn_q${qId}_${subKey}_false`);
      btnTrue.classList.toggle("selected-true", val === true);
      btnFalse.classList.toggle("selected-false", val === false);
      updateProgress();
    }

    function isQuestionAnswered(item) {
      const ans = userAnswers[item.id];
      if (!ans) return false;
      if (item.type === "mcq") return Boolean(ans);
      return ["a", "b", "c", "d"].every((k) => typeof ans[k] === "boolean");
    }

    function updateProgress() {
      const doneCount = questions.filter(isQuestionAnswered).length;
      progressEl.textContent = `Đã làm: ${doneCount} / ${questions.length} câu`;
    }

    function gradeQuiz() {
      let score = 0;
      const maxScore = 20;

      questions.forEach((item) => {
        const explainEl = document.getElementById(`explain_${item.id}`);
        explainEl.style.display = "block";

        if (item.type === "mcq") {
          const userAns = userAnswers[item.id] || null;
          const isCorrect = userAns === item.ans;
          if (isCorrect) score += 1;

          explainEl.innerHTML = `
            <div>${isCorrect ? '<span class="correct-text">✓ Chính xác (+1 điểm)</span>' : `<span class="wrong-text">✗ Chưa đúng (+0 điểm)</span> — Đáp án đúng: <strong>${item.ans}</strong>`}</div>
            <div>Giải thích: ${item.explain}</div>
          `;
        } else {
          const ansObj = userAnswers[item.id] || {};
          let subCorrect = 0;
          const details = [];
          ["a", "b", "c", "d"].forEach((subKey) => {
            const subObj = item.statements[subKey];
            const ok = ansObj[subKey] === subObj.ans;
            if (ok) subCorrect += 1;
            details.push(`${subKey}) ${subObj.ans ? "Đúng" : "Sai"} (${ok ? "✓" : "✗"})`);
          });
          const qScore = subCorrect * 0.25;
          score += qScore;

          explainEl.innerHTML = `
            <div><span class="${subCorrect === 4 ? "correct-text" : "wrong-text"}">Đúng ${subCorrect}/4 ý (+${qScore} điểm)</span> — ${details.join(" | ")}</div>
            <div>Giải thích: ${item.explain}</div>
          `;
        }
      });

      const resBox = document.getElementById("result-box");
      resBox.style.display = "block";
      const diemHe10 = ((score / maxScore) * 10).toFixed(2);
      resBox.innerHTML = `
        <strong>Kết quả làm bài:</strong> ${score} / ${maxScore} điểm thô (quy đổi thang 10: <strong>${diemHe10} điểm</strong>).
      `;
      resBox.scrollIntoView({ behavior: "smooth" });
    }

    function resetQuiz() {
      Object.keys(userAnswers).forEach((k) => delete userAnswers[k]);
      renderQuiz();
      document.getElementById("result-box").style.display = "none";
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    renderQuiz();
  </script>
</body>
</html>
