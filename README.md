# Whack-A-Mole - Final Project

使用 **Dev C++** 搭配 **SFML 函式庫** 製作的打地鼠遊戲期末專題報告

---

## 1. 組員資訊
| 學號      | 姓名     |
|-----------|----------|
| 114511073 | 歐彥呈   |
| 114511224 | 林宇謙   |

---

## 2. 專案簡介
本專題使用 Dev C++ 與 SFML 函式庫製作一款 **打地鼠遊戲 (Whack-A-Mole)**。  
玩家可選擇不同的版面大小及遊戲難度，並需要在限定時間內擊中正確的地鼠類型以獲得高分。

遊戲特色在於：

- 多種地鼠類型（加分、扣分、延長時間等）  
- 可選難度與格子尺寸  
- 即時顯示分數、剩餘時間與歷史最高分  
- 遊戲結束後提供重新開始或退出功能  

---

## 3. 系統需求
1. **Dev C++**：版本 4.9.2  
2. **SFML**：版本 2.4.2  
3. **字型**：`arial.ttf` 必須放置於專案目錄中  
4. **圖片資源**：需與程式同一資料夾  
   - Diglett.png  
   - Three_Diglett.png  
   - bad_Diglett.png  
   - Hammer.png  
   - hole.png  
   - bomb.png  
   - timeplus.png  
   - explosion.png  

---
5. 安裝流程與引入SFML
<img width="1659" height="872" alt="image" src="https://github.com/user-attachments/assets/71bd8c95-e199-48b2-bcde-61f9f98fa5eb" />
選older versions，之後點選2.4.2

<img width="1221" height="706" alt="image" src="https://github.com/user-attachments/assets/be687e40-f02b-44b5-9ed9-4ca86c0ee897" />
然後下載GCC 4.9.2 TDM (SJLJ) - 64-bit這個版本




<img width="1659" height="872" alt="image" src="https://github.com/user-attachments/assets/943dd0e2-6d65-4836-a306-2b9fcca29d87" />

下載完後，在Dev C++裡面的工具裡面的編譯器選項裡的一般中，找到在連結器命令列中加入以下的命令，將-static-libgcc -lsfml-audio -lsfml-graphics -lsfml-system -lsfml-window複製進去







## 4. 遊戲特色與功能

### 4.1 可自訂遊戲板尺寸
| 選項 | 尺寸 |
|------|------|
| A    | 3 × 3 |
| B    | 4 × 4 |

玩家可在遊戲開始時選擇遊戲版面尺寸，決定洞口數量。

---

### 4.2 三種遊戲難度
| 難度  | 特點 |
|-------|------|
| Easy  | 地鼠出現時間較長、速度慢 |
| Normal| 中等速度與反應時間 |
| Hard  | 地鼠快速變換、反應時間極短 |

玩家可在遊戲開始時選擇遊戲難度。

---

### 4.3 多種類型地鼠
| 類型 | 效果 |
|------|------|
| ⭐ 超好地鼠 | 高分加成 (+3分) |
| 👍 好地鼠   | 一般得分 (+1分) |
| 👎 壞地鼠   | 扣分 (-1分) |
| 💣 炸彈     | 觸碰扣大量分數 (-3分) 並有爆炸動畫 |
| ⏱ 時鐘     | 增加遊戲剩餘時間 (+1秒) |

---

### 4.4 即時資訊顯示
遊戲畫面會即時顯示：

- 目前分數 (Current Score)  
- 歷史最高分 (Best Score)  
- 剩餘時間 (Time left)  
- 立即離開按鈕 (Exit)  

---

### 4.5 遊戲結束畫面
遊戲結束後會即時顯示：

- Success (成功！達成指定分數)  
- Failure (失敗，未達成指定分數)  
- 按 `R` 可重新開始，按 `Q` 則退出遊戲  

成功分數標準：**分數 ≥ 20 分**。

---

## 5. 遊戲流程
1. **開始畫面**  
   - 選擇板面尺寸（A=3x3, B=4x4）  
   - 選擇遊戲難度（1=Easy, 2=Normal, 3=Hard）  
   - 按 Enter 開始遊戲  

2. **遊戲進行中**  
   - 玩家使用 **WASD** 移動到目標洞口  
   - 按 **空白鍵** 鎚擊地鼠或道具  
   - 計時器從 30 秒開始倒數  
   - 撞到不同地鼠/道具會對分數或時間產生影響  

3. **遊戲結束**  
   - 當剩餘時間 = 0 或達成分數目標  
   - 顯示成功或失敗訊息  
   - 可選擇重新開始 (`R`) 或退出遊戲 (`Q`)  

---

## 6. 程式架構

### 6.1 檔案結構
/Whack-A-Mole
│ main.cpp
│ arial.ttf
│ highscore.txt
│ Diglett.png
│ Three_Diglett.png
│ bad_Diglett.png
│ Hammer.png
│ hole.png
│ bomb.png
│ timeplus.png
│ explosion.png

yaml
複製程式碼

### 6.2 主要程式邏輯
- **main.cpp**  
  - Start Menu: 選擇 Grid 與 Difficulty  
  - Game Loop:  
    - 更新地鼠出現與消失  
    - 計時器倒數  
    - 玩家操作 (WASD 移動, 空白鍵擊打)  
    - 計算分數與效果  
    - 更新爆炸動畫  
  - Result Screen: 顯示成功/失敗與分數  

### 6.3 主要結構體與類別
| 結構 | 功能 |
|------|------|
| `Mole` | 存放地鼠狀態與類型 |
| `Player` | 玩家位置 (r,c) |
| `Explosion` | 爆炸動畫 |
| `GameState` | MENU / GAME / RESULT |
| `Level` | EASY / NORMAL / HARD |

### 6.4 核心邏輯
- **地鼠出現機率**由難度決定  
- **計時器**從 30 秒倒數，遇到時鐘加 1 秒  
- **分數判定**  
  - 超好地鼠 +3  
  - 好地鼠 +1  
  - 壞地鼠 -1  
  - 炸彈 -3  
  - 時鐘 +1 秒  
- **遊戲成功條件**：分數 ≥ 20  

---

## 7. 編譯與執行說明
1. 使用 **Dev C++ 4.9.2** 開啟專案  
2. 將 **SFML 2.4.2** 設定加入 Dev C++  
   - include 路徑：`SFML/include`  
   - lib 路徑：`SFML/lib`  
3. 確保 `arial.ttf` 與所有圖片在專案目錄  
4. 編譯 `main.cpp`  
5. 執行 EXE  

---

## 8. 資源來源
- 地鼠圖片：自製或公開授權素材  
- 音效與動畫：自製或自由授權  

---

## 9. 遊戲截圖（示意）
> **註**：因 GitHub 限制，請自行放置 `screenshots/` 資料夾  
>  - start_screen.png  
>  - game_screen.png  
>  - result_screen.png  

---

## 10. Bonus 功能
- 可選 **Easy / Normal / Hard**  
- 炸彈與時鐘道具  
- 4×4 grid mode  
- 即時離開按鈕  
- 優化 UI 顯示  

---

## 11. 遊戲操作
| 操作 | 功能 |
|------|------|
| W / A / S / D | 上 / 左 / 下 / 右 移動 |
| 空白鍵        | 鎚擊洞口 |
| R             | 遊戲結束後重新回到選單 |
| Q             | 遊戲結束後退出 |
| 滑鼠點擊 Exit | 立即退出遊戲 |

---

**作者**: 歐彥呈 & 林宇謙  
**專案名稱**: Whack-A-Mole Final Project  

















