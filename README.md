一、啟動後端 (Node.js/Express)
打開終端機 (Terminal / CMD / PowerShell)。
進入後端專案資料夾：
cd path/to/backend

安裝套件：
npm install
2. 啟動開發伺服器：npm run dev
如果使用 nodemon，這會自動監控檔案改動並重新啟動。
預設伺服器會跑在：http://localhost:3001

驗證服務狀態：
curl http://localhost:3001/health
會看到{ "status": "ok" }

二、啟動前端
1. Live Server (HTML + JS)
開啟 VSCode，安裝 Live Server 套件。
滑鼠右鍵按 Go Live。
前端可以直接呼叫後端 API（例如 /api/signup），確保 URL 對應到後端的 http://localhost:3001。

3. Vite
npm install
啟動開發伺服器：npm run dev
終端機會顯示開發網址，例如：Local: http://localhost:5173
打開瀏覽器即可預覽前端。

測試方式
1. Postman / Thunder Client建立 Collection

設定變數：
baseUrl = http://localhost:3001
新增 Request：GET /health → 驗證 200 OK
POST /api/signup → 驗證 201，Body JSON：
{
  "name": "測試同學",
  "email": "test@example.com",
  "phone": "0912345678",
  "password": "abc12345",
  "confirmPassword": "abc12345",
  "interests": ["前端", "後端"],
  "terms": true
}

在 Tests Script 驗證：
pm.test('狀態碼 201', () => pm.response.to.have.status(201));
pm.test('回應包含 participant', () => {
    pm.expect(pm.response.json()).to.have.property('participant');
});
