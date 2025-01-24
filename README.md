# **UbuntuEK_Card_data** 💳

## 1. **프로젝트 개요: 카드 데이터 분석의 필요성과 목표**

### 1.1 카드 데이터 처리 시각화 목적
- 현대의 기업들은 방대한 양의 카드 거래 데이터를 처리하고 분석하는 데 있어 효율적인 방법을 찾고 있습니다. 

- 카드 거래 데이터는 고객 행동 분석, 결제 패턴 추적, 그리고 서비스 최적화를 위한 중요한 인사이트를 제공합니다. 

- 약 520만 개의 데이터를 효과적으로 처리하고 시각화하는 것은 기업의 의사결정과 비즈니스 전략에 중요한 영향을 미칩니다.

### 1.2 기대 효과

- 정확한 비즈니스 인사이트 제공: 실시간 데이터 분석을 통해 카드 사용 패턴, 고객 행동, 결제 트렌드 등을 파악합니다.

- 빠른 의사결정 지원: 실시간 대시보드와 시각화를 통해 데이터 기반의 빠른 의사결정을 지원합니다.

- 운영 효율성 향상: 데이터 처리 속도와 정확도를 높여 비즈니스 운영 효율성을 향상시킵니다.

## 2. **시스템 아키텍처 및 데이터 흐름**

### 2.1 Technology Stack

| Category                  | Technology                                                                 |
|---------------------------|---------------------------------------------------------------------------|
| 🌍 **Operating System**    | ![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=white) ![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white) |
| 📦 **Data Storage & Search** | ![Elasticsearch](https://img.shields.io/badge/Elasticsearch-0052CC?style=for-the-badge&logo=elasticsearch&logoColor=white) |
| 📊 **Data Visualization**  | ![Kibana](https://img.shields.io/badge/Kibana-0052CC?style=for-the-badge&logo=kibana&logoColor=white) |\

<br>
<br>

### 2.2 Technical Architecture and Process Flow
![_- visual selection (1)](https://github.com/user-attachments/assets/80ba4352-ab5a-4dce-b154-d2502bf3dec2)



## 3. **Ubuntu 서버에 ELK 스택 연결 및 구성 과정**
    
### 3.1 Ubuntu & EK Stack version 

![image](https://github.com/user-attachments/assets/61529d46-8bfa-45dc-9833-881f716554ea)

- Ubuntu 연결

``` 
ubuntu@myserver1:~$ curl -X GET "http://localhost:9200" | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   534  100   534    0     0   4979      0 --:--:-- --:--:-- --:--:--  4990
{
  "name": "myserver1",
  "cluster_name": "elasticsearch",
  "cluster_uuid": "EggUzGNoQ-ecUkglI1hpbw",
  "version": {
    "number": "8.17.1" # Ubuntu에 8.xx 최신 버전이 설치되어 있었습니다.
    ...
  }
}
```

## 🔄 Elasticsearch 버전 변경 (8.17.1 → 7.11.1)

하나의 Ubuntu 서버에서 Elasticsearch 버전을 **8.17.1에서 7.11.1로 변경**하기 위해  
패키지를 설치한 후 덮어쓰기 방식으로 다운그레이드를 진행하였습니다.

---

### 📌 변경 결과

![Elasticsearch Installation Step 1](https://github.com/user-attachments/assets/16472c9b-3aba-482a-8907-fc24067ca5aa)

![Elasticsearch Installation Step 2](https://github.com/user-attachments/assets/fddc7970-a4f3-41fd-85eb-4f570a81cdd8)


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Elasticsearch 7.11.1로 변경하는 방법</title>
    <style>
        code {
            background-color: #f4f4f4;
            padding: 5px;
            border-radius: 4px;
        }
        pre {
            background-color: #333;
            color: white;
            padding: 15px;
            border-radius: 4px;
            overflow-x: auto;
            font-family: monospace;
        }
        img {
            max-width: 100%;
            height: auto;
            margin-top: 20px;
            display: block;
            margin-left: auto;
            margin-right: auto;
        }
    </style>
</head>
<body>
    <h1>🚀 Elasticsearch 7.11.1로 다운그레이드하는 방법</h1>
    <h3>1. 현재 설치된 버전 확인</h3>
    <pre><code>dpkg -l | grep elasticsearch</code></pre>
    <p>현재 설치된 버전이 7.11.1이 아닌 경우, 아래 단계를 진행하세요.</p>
    <h3>2. Elasticsearch 7.11.1 패키지 다운로드</h3>
    <pre><code>wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.11.1-amd64.deb</code></pre>
    <h3>3. 기존 버전을 덮어쓰기하여 7.11.1로 설치</h3>
    <pre><code>sudo dpkg -i elasticsearch-7.11.1-amd64.deb</code></pre>
    <p>이 명령어는 기존 버전을 삭제하지 않고 덮어쓰기 설치합니다.</p>
    <h3>4. Elasticsearch 서비스 재시작</h3>
    <pre><code>sudo systemctl restart elasticsearch</code></pre>
    <pre><code>sudo systemctl status elasticsearch</code></pre>
    <h3>5. 새로운 버전 확인</h3>
    <pre><code>curl -X GET "http://localhost:9200" | jq</code></pre>
    <p>또는</p>
    <pre><code>/usr/share/elasticsearch/bin/elasticsearch --version</code></pre>
    <h3>출력 예시:</h3>
    <pre><code>Version: 7.11.1, Build: default/deb/ff1705b/2021-02-15T13:44:09.394032Z, JVM: 11.0.11</code></pre>
    <p>Ubuntu 24.04에 ElasticSearch 7.11.1 version 설치</p>
    <!-- 이미지 삽입 -->
    <img src="https://github.com/user-attachments/assets/865723f1-b46c-42b7-906e-174233a28100" alt="ElasticSearch 7.11.1 동작">
     <pre><code>ElasticSearch 7.11.1 version active</code></pre>
</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kibana 설치 및 설정</title>
    <style>
        img {
            max-width: 100%;
            height: auto;
            margin-top: 20px;
            display: block;
            margin-left: auto;
            margin-right: auto;
        }
        pre {
            background-color: #333;
            color: white;
            padding: 15px;
            border-radius: 4px;
            overflow-x: auto;
            font-family: monospace;
        }
        code {
            background-color: #f4f4f4;
            padding: 5px;
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <h1>🚀 Kibana 설치 및 설정</h1>
    <h3>1. Kibana 설치 준비</h2>
    <p>먼저, Kibana는 Elasticsearch와 연동되므로 Elasticsearch가 정상적으로 설치되고 실행되고 있어야 합니다. Elasticsearch 7.11.1이 실행 중이라면 Kibana 설치를 진행할 수 있습니다.</p>
    <h3>2. Kibana 7.11.1 패키지 다운로드</h2>
    <p>Kibana 7.11.1을 설치하려면, 해당 버전의 .deb 패키지를 다운로드해야 합니다.</p>
    <pre><code>wget https://artifacts.elastic.co/downloads/kibana/kibana-7.11.1-amd64.deb</code></pre>
    <h3>3. Kibana 패키지 설치</h2>
    <p>다운로드한 .deb 파일을 사용해 Kibana를 설치합니다.</p>
    <pre><code>sudo dpkg -i kibana-7.11.1-amd64.deb</code></pre>
    <p>설치가 완료되면 Kibana 서비스가 시스템에 추가됩니다.</p>
    <h3>4. Kibana 설정 파일 수정</h2>
    <p>Kibana의 설정 파일은 <code>/etc/kibana/kibana.yml</code>에 위치해 있습니다. 이 파일을 수정하여 Elasticsearch와의 연결을 설정해야 합니다.</p>
    <pre><code>sudo vi /etc/kibana/kibana.yml</code></pre>
    <h3>server.host 설정</h3>
    <p>기본적으로 Kibana는 localhost로만 접근이 가능하도록 설정됩니다. 원격에서 접근하려면 <code>server.host</code>를 수정해야 합니다.</p>
    <pre><code>server.host: "0.0.0.0"   # 모든 네트워크 인터페이스에서 접근 가능하게 설정</code></pre>
    <h3>elasticsearch.hosts 설정</h3>
    <p>Kibana가 Elasticsearch와 연결할 수 있도록 설정합니다. Elasticsearch의 IP 주소와 포트를 지정해야 합니다.</p>
    <pre><code>elasticsearch.hosts: ["http://localhost:9200"]  # Elasticsearch 서버가 로컬에 있을 경우</code></pre>
    <p>만약 Kibana가 원격 서버에서 실행되고 있고 Elasticsearch가 다른 서버에서 실행 중이라면, Elasticsearch의 IP 주소를 입력합니다:</p>
    <pre><code>elasticsearch.hosts: ["http://<elasticsearch-server-ip>:9200"]</code></pre>
    <h3>5. Kibana 서비스 시작</h2>
    <p>설정 파일을 수정한 후, Kibana 서비스를 시작합니다.</p>
    <pre><code>sudo systemctl start kibana</code></pre>
    <h3>6. Kibana 서비스 자동 시작 설정</h2>
    <p>시스템 부팅 시 Kibana가 자동으로 시작되도록 설정하려면 아래 명령어를 실행합니다.</p>
    <pre><code>sudo systemctl enable kibana</code></pre>
    <h3>7. Kibana 상태 확인</h2>
    <p>Kibana 서비스가 정상적으로 시작되었는지 확인하려면 아래 명령어를 사용합니다.</p>
    <pre><code>sudo systemctl status kibana</code></pre>
    <p>정상적으로 실행 중이라면 Kibana에 접근할 수 있습니다.</p>
    <h3>8. 브라우저에서 Kibana 접속</h2>
    <p>Kibana가 정상적으로 실행되면, 브라우저에서 아래 URL을 통해 Kibana 대시보드에 접근할 수 있습니다:</p>
    <pre><code>http://<서버의 IP 주소>:5601</code></pre>
    <!-- 이미지 삽입 -->
    <img src="https://github.com/user-attachments/assets/e6f16d0a-aa9e-496d-8e2e-47c3b0ba84b5" alt="Kibana Setup Image">
    <pre><code>Kibana 7.11.1 version active</code></pre>
    <p>ElasticSearch 데이터 시각화를 위한 Kibana 7.11.1 version 설치</p>
</body>
</html>

***

### **포트 포워딩 과정**  
VirtualBox에서 설정한 포트 포워딩을 통해 **Elasticsearch**와 **Kibana**에 접속할 수 있었습니다. 아래 이미지는 포트 포워딩을 통해 연결한 결과입니다.

#### **Elasticsearch 접속 성공**  
포트 9200을 사용하여 Elasticsearch에 접속할 수 있음을 확인했습니다.

![image1](https://github.com/user-attachments/assets/d2e5ec74-fc8e-429f-8013-779a77ae7d4e)  

#### **Kibana 접속 성공**  
포트 5601을 통해 Kibana 대시보드에 정상적으로 접속할 수 있음을 확인했습니다.

![image2](https://github.com/user-attachments/assets/b25db30b-e593-49ea-afff-aa4c82d50040)  
***
## 4. Kibana를 통한 카드 데이터 시각화 구현

### 4.1 연령대 카드 이용금액 (1,000 won)
![연령대 카드 이용금액](https://github.com/user-attachments/assets/13c3599b-a6f6-41e9-8ce6-365992b5e91b)

**이점:** 고객층의 연령대 분포를 확인하여, 특정 연령대에 맞춘 마케팅 전략을 세울 수 있습니다. 예를 들어, 젊은 층이 주로 사용하는 카드를 찾으면 이들을 대상으로 하는 프로모션이나 광고를 계획할 수 있습니다.

### 4.2 성별 카드 이용금액 (1: 남성 / 2: 여성)
![성별 카드 이용금액](https://github.com/user-attachments/assets/36f44815-3072-47cd-ab37-34e5f86c0ad2)

**이점:** 고객의 성별에 따른 소비 패턴이나 선호도를 분석할 수 있습니다. 성별에 맞춘 제품 추천 또는 맞춤형 광고 전략을 세울 수 있습니다.

### 4.3 월별 카드 사용 패턴 (2022년 1분기 ~ 2023년 4분기)
![월별 카드 사용 패턴](https://github.com/user-attachments/assets/8d47d570-8663-4f65-87ce-95261c9cccf6)

**이점:** 시간에 따라 카드 사용 패턴을 확인하고, 특정 시즌이나 날짜에 높은 사용률을 보인다면 해당 기간에 맞춘 프로모션을 계획할 수 있습니다.

### 4.4 연령대 체크카드와 신용카드 평균 사용값 비교
![연령대 체크카드와 신용카드 평균 사용값 비교](https://github.com/user-attachments/assets/51030dc1-a74c-4e1d-98d9-5e793202a6af)

**이점:** 특정 연령대에 맞는 카드를 제공하는 것이 중요해집니다. 예를 들어, 20대와 30대는 할인 혜택이 많은 신용카드를 선호할 수 있으며, 40대 이상은 체크카드를 통해 예산 관리를 중시할 수 있습니다. 이를 바탕으로 맞춤형 프로모션이나 카드를 설계할 수 있습니다.

## 시각화를 이용한 신규 카드 이벤트 아이디어

### 1. 연령대별 맞춤형 프로모션

```
- 대상: 20대, 30대
- 이벤트 아이디어: 
  - 젊은 층에서 많이 사용되는 카드에 대해, 할인 혜택이나 캐시백을 제공하는 이벤트 진행.
  - 예시: 주말 쇼핑 할인, 인기 있는 카페나 음식점에서 할인 쿠폰 제공.
- 목표: 젊은 층의 카드 사용률 증가.
```

### 2. 성별 맞춤형 카드 추천 및 이벤트

```
- 대상: 남성 / 여성
- 이벤트 아이디어: 
  - 성별에 맞는 카드 혜택 차별화.
  - 예시: 여성 고객을 대상으로 뷰티/패션 브랜드 할인 이벤트, 남성 고객을 대상으로 기술 제품 할인 이벤트 진행.
- 목표: 각 성별의 선호를 반영한 맞춤형 혜택 제공.
```

### 3. 시즌별 카드 사용 패턴에 맞춘 이벤트

```
- 대상: 전 연령대
- 이벤트 아이디어: 
  - 카드 사용 패턴을 월별로 분석하여, 연말이나 명절 시즌에 맞춰 특별한 포인트 적립이나 할인 혜택 제공.
  - 예시: 연말 쇼핑 시즌에 맞춰 카드 사용액에 따라 포인트 두 배 적립 이벤트.
- 목표: 시즌에 맞춘 전략적 프로모션.
```

### 4. 연령대별 체크카드와 신용카드 혜택 차별화

```
- 대상: 20대~30대 vs 40대 이상
- 이벤트 아이디어: 
  - 20대~30대: 신용카드 선호 연령대에 대해 주요 온라인 쇼핑몰 할인, 영화/여행 예약 시 할인 혜택 제공.
  - 40대 이상: 체크카드 사용 시 가계부 앱 무료 제공, 정기 결제 할인 이벤트.
- 목표: 연령대에 맞춘 카드 혜택 제공하여 사용 증대.
```

### 5. 카드 사용 증대 이벤트

```
- 대상: 전 연령대
- 이벤트 아이디어: 
  - 카드 사용량 증가를 목표로 월간/주간 사용 목표 달성 이벤트 진행.
  - 예시: 월별 특정 금액 초과 사용 시 추첨을 통한 경품 제공, 특별 포인트 지급 이벤트.
- 목표: 카드 사용 촉진.
```

***

## 5. **TroubleShooting**

### **5.1. 데이터 파일 분할**

약 520만 개의 카드 데이터 **edu_data_F_sample.csv** 파일을 **10만 개씩** 나누기 위해, PowerShell 명령어를 사용하여 파일을 분할하였습니다.

```powershell
$inputFile = "C:\path\to\edu_data_F_sample.csv"
$outputDir = "C:\path\to\output\folder"
$linesPerFile = 100000

# 입력 파일을 읽고 나누기
$lines = Get-Content $inputFile
$header = $lines[0]  # 헤더 저장
$lines = $lines[1..$($lines.Length - 1)]  # 데이터만 추출

# 데이터를 10만 개씩 나누기
$index = 0
foreach ($i in 0..([math]::Ceiling($lines.Length / $linesPerFile) - 1)) {
    $startIndex = $i * $linesPerFile
    $endIndex = [math]::Min(($i + 1) * $linesPerFile - 1, $lines.Length - 1)
    $chunk = $lines[$startIndex..$endIndex]

    # 새로운 파일 생성
    $chunk | Set-Content -Path "$outputDir\chunk_$index.csv"
    $index++
}
```

***

![image3](https://github.com/user-attachments/assets/e4858f69-8c22-4007-9a7f-51c386451978)
``` 
edu_data_F_sample.csv 파일 분할
 ```
***

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Elasticsearch 서비스 시작 오류 해결</title>
</head>
<body>
    <h2>5.2. Elasticsearch 서비스 시작 오류 해결</h2>
    <h3>문제 상황</h3>
    <p>`sudo systemctl restart elasticsearch` 명령어를 실행했을 때, Elasticsearch 서비스가 실패하며 다음과 같은 오류 메시지가 출력되었습니다:</p>
    <pre>
Job for elasticsearch.service failed because the control process exited with error code
See "systemctl status elasticsearch.service" and "journalctl -xeu elasticsearch" for details.
    </pre>
    <h3>해결 방법</h3>
    <ol>
        <li><strong>서비스 상태 확인</strong><br>
            <p>`systemctl status elasticsearch.service` 명령어를 통해 Elasticsearch 서비스의 상태를 확인합니다. 이를 통해 서비스 실패 원인에 대한 자세한 정보를 얻을 수 있습니다.</p>
        </li>
        <li><strong>로그 확인</strong><br>
            <p>`journalctl -xeu elasticsearch` 명령어를 사용하여 Elasticsearch와 관련된 시스템 로그를 확인합니다. 로그에서 에러 메시지나 경고를 찾아 문제를 파악합니다.</p>
        </li>
        <li><strong>설정 확인</strong><br>
            <p>`elasticsearch.yml` 파일에서 `discovery.type` 설정을 확인하고, 적절하게 수정합니다. 예를 들어, 클러스터 구성을 단일 노드로 설정하는 방법은 다음과 같습니다:<p>
            <pre>
네트워크 설정
    network.host: 0.0.0.0

클러스터 설정
    discovery.type: single-node
            </pre>
        </li>
        <li><strong>서비스 재시작</strong><br>
            <p>설정을 수정한 후, sudo systemctl restart elasticsearch 명령어로 서비스를 재시작합니다.</p>
        </li>
    </ol>
    <h3>결과</h3>
    <p>위의 과정을 통해 서비스가 정상적으로 시작되었습니다.</p>
</body>
</html>

![image4](https://github.com/user-attachments/assets/aa4d73ef-2559-47a7-b659-934dc5785c68)

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Elasticsearch Keystore 포맷 오류 해결</title>
</head>
<body>
    <h2>5.3. 문제: Elasticsearch Keystore 포맷 오류</h1>
    <p><strong>오류 메시지:</strong></p>
    <pre>
Exception in thread "main" java.lang.IllegalStateException: The Elasticsearch keystore [/etc/elasticsearch/elasticsearch.keystore] format is too new. Are you trying to downgrade? You should delete and recreate it in order to downgrade.
...
Caused by: org.apache.lucene.index.IndexFormatTooNewException: Format version is not supported (resource BufferedChecksumIndexInput(SimpleFSIndexInput(path="/etc/elasticsearch/elasticsearch.keystore"))): 6 (needs to be between 1 and 4)
    </pre>
    <p><strong>문제 설명:</strong></p>
    <p>Elasticsearch keystore의 포맷 버전이 너무 최신 버전으로 설정되어, 현재 설치된 버전(7.11.1)과 호환되지 않아 다운그레이드 시 오류가 발생하였습니다.</p>
    <h3>해결 방법</h3>
    <ol>
        <li>
            <strong>Elasticsearch 서비스 중지</strong><br>
            Elasticsearch를 중지하여 keystore 파일을 수정할 수 있는 상태로 만듭니다.
            <pre><code>sudo systemctl stop elasticsearch</code></pre>
        </li>
        <li>
            <strong>기존 keystore 파일 삭제</strong><br>
            현재 오류를 발생시키는 기존 keystore 파일을 삭제합니다.
            <pre><code>sudo rm -f /etc/elasticsearch/elasticsearch.keystore</code></pre>
        </li>
        <li>
            <strong>새로운 keystore 파일 생성</strong><br>
            Elasticsearch는 keystore 파일을 새로 생성할 수 있습니다. 새로 생성하려면 아래 명령어를 사용합니다.
            <pre><code>sudo /usr/share/elasticsearch/bin/elasticsearch-keystore create</code></pre>
        </li>
        <li>
            <strong>Elasticsearch 서비스 재시작</strong><br>
            새로운 keystore 파일이 생성되었으면, Elasticsearch 서비스를 재시작합니다.
            <pre><code>sudo systemctl start elasticsearch</code></pre>
        </li>
        <li>
            <strong>Elasticsearch 상태 확인</strong><br>
            서비스가 정상적으로 시작되었는지 확인합니다.
            <pre><code>sudo systemctl status elasticsearch</code></pre>
        </li>
        <li>
            <strong>버전 확인</strong><br>
            Elasticsearch가 정상적으로 실행 중이라면, 버전을 확인하여 문제가 해결되었는지 확인합니다.
            <pre><code>curl -X GET "http://localhost:9200" | jq</code></pre>
            또는
            <pre><code>/usr/share/elasticsearch/bin/elasticsearch --version</code></pre>
        </li>
    </ol>
    <h3>결론</h3>
    <p>위의 절차를 통해 Elasticsearch keystore 파일의 문제를 해결하고, 정상적으로 서비스가 실행하였습니다.</p>
    <p>이 트러블슈팅 문서를 통해 해당 문제를 효과적으로 해결하였습니다.</p>
</body>
</html>


***

## 6. **Review**

    
1. 성능 최적화
520만 개 이상의 데이터를 관리하는 데 있어서 성능적인 측면을 고려하는 것이 중요하다고 생각합니다. 데이터 분석을 위한 쿼리나 처리 속도를 최적화하여 시스템이 원활하게 돌아갈 수 있도록 관리하는 방법을 개선해야 한다는 점을 깨닫게 되었습니다.

<br>

2. 확장성 및 유지보수성
데이터가 추가되거나 업데이트될수록 시스템의 확장성을 고려해야 합니다. 특히 카드 데이터를 분석하는 데 있어 성능 저하가 발생하지 않도록, Elasticsearch(ES) 설정을 최적화하고 튜닝을 고도화해야 할 필요성이 커졌습니다.

<br>

3. 데이터 자동화
카드 데이터는 자동으로 처리되는 것이 중요한 만큼, Logstash를 활용하여 자동화된 데이터 수집 및 처리 파이프라인을 구축할 계획입니다. 또한, Elasticsearch의 알림 기능을 통해 데이터 변경 사항을 실시간으로 파악할 수 있도록 시스템을 개선할 예정입니다.
