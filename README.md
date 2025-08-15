# Nacos Waiter Service ⚡

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.4-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2023.0.1-blue.svg)](https://spring.io/projects/spring-cloud)
[![Spring Cloud Alibaba](https://img.shields.io/badge/Spring%20Cloud%20Alibaba-2023.0.1.0-red.svg)](https://github.com/alibaba/spring-cloud-alibaba)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 專案介紹

這是一個基於 Spring Cloud Alibaba Nacos 的服務註冊與發現示範專案，展示如何在微服務架構中使用 Nacos 作為服務註冊中心。專案實現了一個咖啡廳服務系統，包含服務註冊、服務發現、負載均衡等核心功能。

### 🎯 專案特色

- **服務註冊與發現**：使用 Nacos 實現服務的自動註冊和發現
- **負載均衡**：整合 Spring Cloud LoadBalancer 實現服務調用的負載均衡
- **健康檢查**：提供完整的服務健康狀態監控
- **配置管理**：支援動態配置更新和服務配置管理
- **監控指標**：整合 Micrometer 和 Prometheus 提供詳細的監控指標

### 💡 為什麼選擇此專案？

- **學習價值**：完整展示微服務架構中的服務註冊與發現機制
- **實用性**：提供可直接運行的咖啡廳業務場景
- **現代化**：使用最新的 Spring Boot 3.x 和 Spring Cloud 2023.x 版本
- **可擴展性**：架構設計支援後續功能擴展

## 技術棧

### 核心框架
- **Spring Boot 3.2.4** - 現代化的 Java 應用程式框架
- **Spring Cloud 2023.0.1** - 微服務架構解決方案
- **Spring Cloud Alibaba 2023.0.1.0** - 阿里巴巴微服務生態系統
- **Spring Data JPA** - 資料持久化框架

### 服務註冊與發現
- **Nacos 2.3.2** - 動態服務發現、配置管理和服務管理平台
- **Spring Cloud LoadBalancer** - 客戶端負載均衡器

### 開發工具與輔助
- **H2 Database** - 內嵌式記憶體資料庫
- **Lombok** - 減少樣板程式碼
- **Micrometer** - 應用程式監控指標收集
- **Prometheus** - 監控系統

## 專案結構

```
nacos-waiter-service/
├── src/
│   ├── main/
│   │   ├── java/tw/fengqing/spring/springbucks/waiter/
│   │   │   ├── WaiterServiceApplication.java          # 主應用程式類別
│   │   │   ├── controller/                            # REST API 控制器
│   │   │   │   ├── CoffeeController.java             # 咖啡管理 API
│   │   │   │   ├── CoffeeOrderController.java        # 訂單管理 API
│   │   │   │   └── PerformanceInteceptor.java        # 效能監控攔截器
│   │   │   ├── model/                                # 資料模型
│   │   │   │   ├── BaseEntity.java                   # 基礎實體類別
│   │   │   │   ├── Coffee.java                       # 咖啡實體
│   │   │   │   ├── CoffeeOrder.java                  # 訂單實體
│   │   │   │   └── OrderState.java                   # 訂單狀態列舉
│   │   │   ├── repository/                           # 資料存取層
│   │   │   │   ├── CoffeeRepository.java             # 咖啡資料存取
│   │   │   │   └── CoffeeOrderRepository.java        # 訂單資料存取
│   │   │   ├── service/                              # 業務邏輯層
│   │   │   │   ├── CoffeeService.java                # 咖啡業務邏輯
│   │   │   │   └── CoffeeOrderService.java           # 訂單業務邏輯
│   │   │   └── support/                              # 支援類別
│   │   │       ├── CoffeeIndicator.java              # 健康檢查指標
│   │   │       └── MoneySerializer.java              # 貨幣序列化器
│   │   └── resources/
│   │       ├── application.properties                # 應用程式配置
│   │       ├── bootstrap.properties                  # 啟動配置
│   │       ├── schema.sql                            # 資料庫結構
│   │       └── data.sql                              # 初始資料
│   └── test/                                         # 測試程式碼
├── pom.xml                                           # Maven 專案配置
└── README.md                                         # 專案說明文件
```

## 快速開始

### 前置需求

- **Java 21** - 確保已安裝 JDK 21 或更高版本
- **Maven 3.6+** - 專案建置工具
- **Nacos Server** - 服務註冊中心（可選，目前配置為禁用狀態）

### 安裝與執行

1. **克隆此倉庫：**
```bash
git clone https://github.com/SpringMicroservicesCourse/spring-microservices-course.git
cd spring-microservices-course/Chapter\ 12\ 服務註冊與發現/nacos-waiter-service
```

2. **編譯專案：**
```bash
mvn clean compile
```

3. **執行應用程式：**
```bash
mvn spring-boot:run
```

4. **驗證服務：**
```bash
# 檢查應用程式健康狀態
curl http://localhost:8080/actuator/health

# 獲取所有咖啡
curl http://localhost:8080/coffee/

# 創建新訂單
curl -X POST http://localhost:8080/order/ \
  -H "Content-Type: application/json" \
  -d '{"customer":"張三","items":["latte","americano"]}'
```

## 進階說明

### 環境變數

```properties
# Nacos 服務註冊中心配置（目前禁用）
spring.cloud.nacos.discovery.enabled=false
spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848

# 資料庫配置
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=none

# 監控配置
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

### 重要配置說明

```properties
# application.properties 主要設定
# 服務註冊配置 - 目前暫時禁用以避免 Nacos 連接問題
spring.cloud.nacos.discovery.enabled=false

# JPA 配置 - 使用 H2 記憶體資料庫
spring.jpa.hibernate.ddl-auto=none
spring.jpa.properties.hibernate.show_sql=true

# Actuator 配置 - 啟用所有監控端點
management.endpoints.web.exposure.include=*
```

## API 端點說明

### 咖啡管理 API

| 方法 | 端點 | 說明 | 範例 |
|------|------|------|------|
| GET | `/coffee/` | 獲取所有咖啡 | `curl http://localhost:8080/coffee/` |
| GET | `/coffee/{id}` | 根據 ID 獲取咖啡 | `curl http://localhost:8080/coffee/1` |
| GET | `/coffee/?name={name}` | 根據名稱獲取咖啡 | `curl http://localhost:8080/coffee/?name=latte` |
| POST | `/coffee/` | 新增咖啡 | `curl -X POST http://localhost:8080/coffee/ -d "name=latte&price=50"` |

### 訂單管理 API

| 方法 | 端點 | 說明 | 範例 |
|------|------|------|------|
| GET | `/order/{id}` | 獲取訂單詳情 | `curl http://localhost:8080/order/1` |
| POST | `/order/` | 創建新訂單 | `curl -X POST http://localhost:8080/order/ -H "Content-Type: application/json" -d '{"customer":"張三","items":["latte"]}'` |

### 監控端點

| 端點 | 說明 |
|------|------|
| `/actuator/health` | 應用程式健康狀態 |
| `/actuator/info` | 應用程式資訊 |
| `/actuator/metrics` | 監控指標 |

## 參考資源

- [Spring Boot 官方文件](https://spring.io/projects/spring-boot)
- [Spring Cloud 官方文件](https://spring.io/projects/spring-cloud)
- [Spring Cloud Alibaba 官方文件](https://github.com/alibaba/spring-cloud-alibaba)
- [Nacos 官方文件](https://nacos.io/zh-cn/docs/what-is-nacos.html)
- [微服務架構實戰課程](https://blog.fengqing.tw/)

## 注意事項與最佳實踐

### ⚠️ 重要提醒

| 項目 | 說明 | 建議做法 |
|------|------|----------|
| 服務註冊 | Nacos 連接問題 | 目前暫時禁用，可根據需要啟用 |
| 資料庫 | 使用 H2 記憶體資料庫 | 生產環境建議使用 PostgreSQL 或 MySQL |
| 監控 | 啟用所有 Actuator 端點 | 生產環境建議只啟用必要端點 |

### 🔒 最佳實踐指南

- **服務註冊**：確保 Nacos 服務器穩定運行，配置適當的重試機制
- **負載均衡**：使用 Spring Cloud LoadBalancer 實現客戶端負載均衡
- **健康檢查**：定期檢查服務健康狀態，及時處理異常
- **監控指標**：整合 Prometheus 和 Grafana 進行監控
- **配置管理**：使用 Nacos 配置中心管理應用程式配置

### 📝 程式碼註解規範

在重要的程式碼區塊添加清楚註解，方便團隊成員理解與維護：

```java
/**
 * 咖啡服務類別
 * 負責處理咖啡相關的業務邏輯，包含新增、查詢、快取等功能
 * 
 * @author 風清雲談
 * @since 2025-01-01
 */
@Service
@Slf4j
@CacheConfig(cacheNames = "CoffeeCache")
public class CoffeeService {
    
    /**
     * 新增咖啡
     * 將新的咖啡資訊儲存到資料庫中
     * 
     * @param name 咖啡名稱，不能為空
     * @param price 咖啡價格，使用 Joda Money 處理貨幣
     * @return 儲存後的咖啡物件
     */
    public Coffee saveCoffee(String name, Money price) {
        // 記錄新增咖啡的操作日誌
        log.info("新增咖啡：{}，價格：{}", name, price);
        
        Coffee coffee = Coffee.builder()
                .name(name)
                .price(price)
                .build();
        
        return coffeeRepository.save(coffee);
    }
}
```

## 授權說明

本專案採用 MIT 授權條款，詳見 LICENSE 檔案。

## 關於我們

我們主要專注在敏捷專案管理、物聯網（IoT）應用開發和領域驅動設計（DDD）。喜歡把先進技術和實務經驗結合，打造好用又靈活的軟體解決方案。

## 聯繫我們

- **FB 粉絲頁**：[風清雲談 | Facebook](https://www.facebook.com/profile.php?id=61576838896062)
- **LinkedIn**：[linkedin.com/in/chu-kuo-lung](https://www.linkedin.com/in/chu-kuo-lung)
- **YouTube 頻道**：[雲談風清 - YouTube](https://www.youtube.com/channel/UCXDqLTdCMiCJ1j8xGRfwEig)
- **風清雲談 部落格**：[風清雲談](https://blog.fengqing.tw/)
- **電子郵件**：[fengqing.tw@gmail.com](mailto:fengqing.tw@gmail.com)

---

**📅 最後更新：2025-01-13**  
**👨‍💻 維護者：風清雲談**
