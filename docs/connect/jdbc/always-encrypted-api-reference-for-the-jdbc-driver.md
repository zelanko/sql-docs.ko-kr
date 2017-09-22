---
title: "상시 암호화는 JDBC 드라이버에 대 한 API 참조 | Microsoft Docs"
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 951172d75cd37687482e1a6ce8ba4476872d2d4b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>상시 암호화는 JDBC 드라이버에 대 한 API 참조
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  상시 암호화를 사용하면 클라이언트가 클라이언트 응용 프로그램의 중요한 데이터를 암호화하고 암호화 키를 SQL Server에 표시하지 않을 수 있습니다. 클라이언트 컴퓨터에 설치된 상시 암호화 지원 드라이버가 SQL Server 클라이언트 응용 프로그램의 중요한 데이터를 자동으로 암호화하고 암호 해독합니다. 드라이버는 데이터를 SQL Server로 전달하기 전에 중요한 열의 데이터를 암호화하고 응용 프로그램에 대한 의미 체계가 유지되도록 자동으로 쿼리를 다시 작성합니다. 마찬가지로, 드라이버는 쿼리 결과에 포함되고 암호화된 데이터베이스 열에 저장된 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 참조 [상시 암호화 (데이터베이스 엔진)](/sql-docs/docs/relational-databases/security/encryption/always-encrypted-database-engine) 및 [상시 암호화와 JDBC 드라이버를 사용 하 여](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)합니다.  
  
> [!NOTE]  
>  상시 암호화는 SQL Server 2016에서 SQL Server 용 Microsoft JDBC Driver 6.0에서만 지원 이상.  
  
 상시 암호화를 사용하는 클라이언트 응용 프로그램에서 사용하기 위해 JDBC 드라이버 API에 몇 가지 새로운 기능이 추가되고 수정되었습니다.  
  
 **SQLServerConnection 클래스**  
  
|이름|설명|  
|----------|-----------------|  
|새 연결 문자열 키워드:<br /><br /> columnEncryptionSetting|columnEncryptionSetting = Enabled 연결과 columnEncryptionSetting에 대해 항상 암호화 기능을 사용 하도록 설정 = 사용 안 함 사용 되지 않습니다. 허용되는 값이 사용/사용 안 함으로 설정되었습니다. 기본값은 Disabled입니다.|  
|새 메서드:<br /><br /> public static void setColumnEncryptionTrustedMasterKeyPaths (지도 < i n g, 목록\<문자열 >> trustedKeyPaths)<br /><br /> public static void updateColumnEncryptionTrustedMasterKeyPaths (서버 문자열 목록\<문자열 > trustedKeyPaths)<br /><br /> public static void removeColumnEncryptionTrustedMasterKeyPaths (문자열 서버)|데이터베이스 서버에 대 한 설정/업데이트/제거 신뢰할 수 있는 키 경로 목록 할 수 있습니다. 응용 프로그램 쿼리를 처리하는 동안 드라이버에서 목록에 없는 키 경로를 수신하면 쿼리가 실패합니다. 이 속성은 손상된 SQL Server가 가짜 키 쌍을 제공하여 키 저장소 자격 증명을 유출하는 보안 공격에 대한 추가 보호를 제공합니다.|  
|새 메서드:<br /><br /> 공용 정적 맵 < i n g, 목록\<문자열 >> getColumnEncryptionTrustedMasterKeyPaths()|데이터베이스 서버에 대한 신뢰할 수 있는 키 경로 목록을 반환합니다.|  
|새 메서드:<br /><br /> public static void registerColumnEncryptionKeyStoreProviders (지도\<SQLServerColumnEncryptionKeyStoreProvider, 문자열 > clientKeyStoreProviders)|사용자 지정 키 저장소 공급자를 등록할 수 있습니다. 키 저장소 공급자 이름을 키 저장소 공급자 구현에 매핑하는 사전입니다.<br /><br /> JVM 키 저장소를 사용하려면 JVM 키 저장소 자격 증명으로 SQLServerColumnEncryptionJVMKeyStoreProvider 개체를 인스턴스화하고 드라이버에 등록해야 합니다. 이 공급자에 대 한 이름 'MSSQL_JVM_KEYSTORE' 이어야 합니다.<br /><br /> Azure 키 자격 증명 모음 저장소를 사용 하려면 SQLServerColumnEncryptionAzureKeyStoreProvider 개체를 인스턴스화하고 드라이버에 등록 해야 합니다. 이 공급자에 대 한 이름 'AZURE_KEY_VAULT' 이어야 합니다.|
|공용 최종 부울 getSendTimeAsDatetime()|SendTimeAsDatetime 연결 속성의 설정을 반환합니다.|
|public void setSendTimeAsDatetime (부울 sendTimeAsDateTimeValue)|SendTimeAsDatetime 연결 속성의 설정을 수정합니다.|

 **SQLServerConnectionPoolProxy 클래스**
|이름|Description|  
|----------|-----------------|  
|공용 최종 부울 getSendTimeAsDatetime()|SendTimeAsDatetime 연결 속성의 설정을 반환합니다.|
|public void setSendTimeAsDatetime (부울 sendTimeAsDateTimeValue)|SendTimeAsDatetime 연결 속성의 설정을 수정합니다.|
     
  
 **SQLServerDataSource 클래스**  
  
|이름|Description|  
|----------|-----------------|  
|public void setColumnEncryptionSetting (문자열 columnEncryptionSetting)|데이터 원본 개체에 대해 상시 암호화 기능을 사용하거나 사용하지 않습니다.<br /><br /> 기본값은 Disabled입니다.|  
|공용 문자열 getColumnEncryptionSetting()|데이터 원본 개체에 대한 상시 암호화 기능 설정을 가져옵니다.|
|public void setKeyStoreAuthentication (문자열 keyStoreAuthentication)|키 저장소를 식별 하는 이름을 설정 합니다. 만 지원 점은 identifiying Java 키 저장소에 대 한 "JavaKeyStorePassword"입니다.<br/><br/>기본값은 null입니다.|
|공용 문자열 getKeyStoreAuthentication()|데이터 원본 개체에 대 한 keyStoreAuthentication 설정의 값을 가져옵니다.|
|public void setKeyStoreSecret (문자열 keyStoreSecret)|Java keystore에 대 한 암호를 설정합니다. Note, Java 키 저장소 공급자에 대 한 키 저장소와 키에 대 한 암호 동일 해야 합니다. keyStoreAuthentication "JavaKeyStorePassword"으로 설정 해야 합니다.|
|public void setKeyStoreLocation (문자열 keyStoreLocation)|Java keystore에 대 한 파일 이름을 포함 한 위치를 설정 합니다. keyStoreAuthentication "JavaKeyStorePassword"으로 설정 해야 합니다.|
|공용 문자열 getKeyStoreLocation()|Java 키 저장소에 대 한 keyStoreLocation를 검색합니다.|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 클래스**  
  
 Java 키 저장소에 대 한 키 저장소 공급자의 구현입니다. 이 클래스는 열 마스터 키로 Java keystore에 저장 된 인증서를 사용할 수 있습니다.  
  
 생성자  
  
|이름|Description|  
|----------|-----------------|  
|공용 SQLServerColumnEncryptionJavaKeyStoreProvider (문자열 keyStoreLocation, char keyStoreSecret)|Java 키 저장소에 대 한 키 저장소 공급자입니다.|  
  
 메서드  
  
|이름|Description|  
|----------|-----------------|  
|공용 바이트 decryptColumnEncryptionKey (문자열 masterKeyPath, 문자열 encryptionAlgorithm, 바이트 encryptedColumnEncryptionKey)|열 암호화 키의 지정된 암호화 값을 암호 해독합니다. 암호화 값은 지정된 키 경로가 있는 인증서와 지정된 알고리즘을 사용하여 암호화해야 합니다.<br /><br /> **키 경로의 형식은 다음 중 하나 여야 합니다.**<br /><br /> 지문:<certificate_thumbprint><br /><br /> 별칭:<certificate_alias><br /><br /> (SQLServerColumnEncryptionKeyStoreProvider 재정의합니다. (String, String, Byte[]).) decryptColumnEncryptionKey|  
|공용 바이트 encryptColumnEncryptionKey (문자열 masterKeyPath, 문자열 encryptionAlgorithm, 바이트 plainTextColumnEncryptionKey)|지정된 키 경로가 있는 인증서와 지정된 알고리즘을 사용하여 열 암호화 키를 암호화합니다.<br /><br /> **키 경로의 형식은 다음 중 하나 여야 합니다.**<br /><br /> 지문:<certificate_thumbprint><br /><br /> 별칭:<certificate_alias><br /><br /> (SQLServerColumnEncryptionKeyStoreProvider 재정의합니다. (String, String, Byte[]).) encryptColumnEncryptionKey|  
|public void setName (문자열 이름)|이 키 저장소 공급자의 이름을 설정합니다.|
|공용 문자열 getName)|이 키 저장소 공급자의 이름을 가져옵니다.|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 클래스**  
  
 Azure 키 자격 증명 모음에 대 한 키 저장소 공급자의 구현입니다. 이 클래스는 열 마스터 키로 Azure 키 자격 증명 모음에 저장 된 키를 사용할 수 있습니다.  
  
 생성자  
  
|이름|Description|  
|----------|-----------------|  
|공용 SQLServerColumnEncryptionAzureKeyVaultProvider (SQLServerKeyVaultAuthenticationCallback authenticationCallback, ExecutorService executorService)|Azure 키 자격 증명 모음에 대 한 키 저장소 공급자입니다.  Azure 키 자격 증명 모음의 키에 대 한 액세스 토큰을 검색 하는 SQLServerKeyVaultAuthenticationCallback 인터페이스에 대 한 구현을 제공 해야 합니다.|  
  
 메서드  
  
|이름|Description|  
|----------|-----------------|  
|공용 바이트 decryptColumnEncryptionKey (문자열 masterKeyPath, 문자열 encryptionAlgorithm, 바이트 encryptedColumnEncryptionKey)|열 암호화 키의 지정된 암호화 값을 암호 해독합니다. 암호화 된 값에서 지정한 열 키 IDmaster 키를 사용 하 여 및 지정된 된 알고리즘을 사용 하 여 암호화 될 예정입니다. <br />(SQLServerColumnEncryptionKeyStoreProvider 재정의합니다. (String, String, Byte[]).) decryptColumnEncryptionKey|  
|공용 바이트 encryptColumnEncryptionKey (문자열 masterKeyPath, 문자열 encryptionAlgorithm, 바이트 columnEncryptionKey)|지정 된 열 마스터 키를 사용 하 고 지정된 된 알고리즘을 사용 하 여 열 암호화 키를 암호화 합니다. <br />(SQLServerColumnEncryptionKeyStoreProvider 재정의합니다. (String, String, Byte[]).) encryptColumnEncryptionKey|  
|public void setName (문자열 이름)|이 키 저장소 공급자의 이름을 설정합니다.|
|공용 문자열 getName)|이 키 저장소 공급자의 이름을 가져옵니다.|  
  
  
 **SQLServerKeyVaultAuthenticationCallback 인터페이스**  
  
 이 인터페이스를 사용자가 구현 해야 하는 Azure 키 자격 증명 모음 인증에 대 한 한 가지 방법은 포함 합니다.  
  
 메서드  
  
|이름|Description|  
|----------|-----------------|  
|공용 문자열 getAccessToken (문자열 기관, 문자열 리소스, 문자열 범위);|메서드를 재정의할 수 있어야 합니다. 메서드 액세스를 Azure 키 자격 증명 모음 토큰을 가져오는 사용 됩니다.|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 클래스**  
  
 사용자 지정 키 저장소 공급자를 구현하려면 이 클래스를 확장합니다.  
  
|이름|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|모든 키 저장소 공급자에 대한 기본 클래스입니다. 사용자 지정 공급자가이 클래스에서 파생 하 고 해당 멤버 함수를 재정의 고 SQLServerConnection을 사용 하 여 다음 등록 해야 합니다. registerColumnEncryptionKeyStoreProviders() 합니다.|  
  
 메서드  
  
|이름|Description|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|열 암호화 키의 지정된 암호화 값을 암호 해독하는 기본 클래스 메서드입니다. 암호화 값은 지정된 키 경로가 있는 열 마스터 키와 지정된 알고리즘을 사용하여 암호화해야 합니다.|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|지정된 키 경로가 있는 열 마스터 키와 지정된 알고리즘을 사용하여 열 암호화 키를 암호화하기 위한 기본 클래스 메서드입니다.|
|공용 추상 void setName (문자열 이름)|이 키 저장소 공급자의 이름을 설정합니다.|
|공용 추상 문자열 getName()|이 키 저장소 공급자의 이름을 가져옵니다.|  
  
 새로 추가 되거나 오버 로드 된 메서드 **SQLServerPreparedStatement** 클래스  
  
|이름|Description|  
|----------|-----------------|  
|public void setBigDecimal (parameterIndex int, int 정밀도 x BigDecimal int 배율)<br /><br /> public void setObject (int parameterIndex, 개체 x, int targetSqlType, 정수 정밀도, 배율 int)<br /><br /> public void setObject (int parameterIndex, 개체 x, SQLType targetSqlType, 정수 정밀도, 배율 정수)<br /><br /> public void setTime (int parameterIndex, x, int 배율 java.sql.Time)<br /><br /> public void setTimestamp (int parameterIndex, x, int 배율 java.sql.Timestamp) <br />public void setDateTimeOffset (int parameterIndex, microsoft.sql.DateTimeOffset x int 배율)|이러한 메서드는 필요한 전체 자릿수 및 소수 자릿수 정보가 특정 데이터 형식에 대 한 상시 암호화를 지원 하기 위해 정밀도 또는 배율 인수 오버 로드 합니다.|  
|public void setMoney (int parameterIndex, BigDecimal x)<br /><br /> public void setSmallMoney (int parameterIndex, BigDecimal x)<br /><br /> public void setUniqueIdentifier (int parameterIndex, guid 문자열)<br /><br /> public void setDateTime (int parameterIndex java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (int parameterIndex java.sql.Timestamp x)|이러한 메서드는 데이터 형식 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime에 대 한 상시 암호화를 지원 하기 위해 추가 됩니다. <br/><br/>암호화 된 datetime2 열에 매개 변수 값을 보내는 데 기존 setTimestamp() 메서드를 사용 하는 참고 합니다. 암호화 된 datetime 및 smalldatetime 열에 대 한 각각의 새 메서드 setDateTime() 및 setSmallDateTime() 사용 합니다.|  
|공용 최종 void setBigDecimal (parameterIndex int, int 정밀도 x BigDecimal, 부울 forceEncrypt int 소수 자릿수)<br /><br /> 공용 최종 void setMoney (int parameterIndex, x, 부울 forceEncrypt BigDecimal)<br /><br /> 공용 최종 void setSmallMoney (int parameterIndex, x, 부울 forceEncrypt BigDecimal)<br /><br /> 공용 최종 void setBoolean (int parameterIndex, 부울 x, 부울 forceEncrypt)<br /><br /> 공용 최종 void setByte (int parameterIndex, x, 부울 forceEncrypt byte)<br /><br /> 공용 최종 void setBytes (int parameterIndex, 바이트 x[], 부울 forceEncrypt)<br /><br /> 공용 최종 void setUniqueIdentifier (int parameterIndex, 문자열 guid, boolean forceEncrypt)<br /><br /> 공용 최종 void setDouble (int parameterIndex, double x, 부울 forceEncrypt)<br /><br /> 공용 최종 void setFloat (int parameterIndex, x float, boolean forceEncrypt)<br /><br /> 공용 최종 void setInt (parameterIndex int, int 값, 부울 forceEncrypt)<br /><br /> 공용 최종 void setLong (int parameterIndex, x long, boolean forceEncrypt)<br /><br /> 공용 최종 setObject (int parameterIndex, 개체 x, int targetSqlType, 정수 정밀도, 배율 int, boolean forceEncrypt)<br /><br /> 공용 최종 void setObject (int parameterIndex, 개체 x, SQLType targetSqlType, 정수 정밀도, 배율 정수, 부울 forceEncrypt)<br /><br /> 공용 최종 void setShort (int parameterIndex, 짧은 x, 부울 forceEncrypt)<br /><br /> 공용 최종 void setString (int parameterIndex, 문자열 str 부울 forceEncrypt)<br /><br /> 공용 최종 void setNString (int parameterIndex, 문자열 값, 부울 forceEncrypt)<br /><br /> 공용 최종 void setTime (int parameterIndex, x, int 배율 java.sql.Time 부울 forceEncrypt)<br /><br /> 공용 최종 void setTimestamp (x, int 비율, java.sql.Timestamp, int parameterIndex 부울 forceEncrypt)<br /><br /> 공용 최종 void setDateTimeOffset (int parameterIndex, x, int 비율, microsoft.sql.DateTimeOffset 부울 forceEncrypt)<br /><br /> 공용 최종 void setDateTime (int parameterIndex, x, 부울 forceEncrypt java.sql.Timestamp)<br /><br /> 공용 최종 void setSmallDateTime (int parameterIndex, x, 부울 forceEncrypt java.sql.Timestamp)<br /><br /> 공용 최종 void setDate (int parameterIndex, java.sql.Date, java.util.Calendar cal x 부울 forceEncrypt)<br /><br /> 공용 최종 void setTime (int parameterIndex, java.sql.Time, java.util.Calendar cal x 부울 forceEncrypt)<br /><br /> 공용 최종 void setTimestamp (int parameterIndex, java.sql.Timestamp, java.util.Calendar cal x 부울 forceEncrypt)|지정된 된 매개 변수를 지정 된 java 값으로 설정합니다.<br /><br /> 부울 forceEncrypt 설정 된 경우 쿼리를 true로 매개 변수는 경우에 설정 지정 열이 암호화 하 고 연결 또는 명령문에 상시 암호화 사용 합니다.<br /><br /> 부울 forceEncrypt가 false로 설정 하는 경우 드라이버는 매개 변수에 대 한 암호화를 요구 하지 않습니다.|  
  
 새로 추가 되거나 오버 로드 된 메서드 **SQLServerCallableStatement** 클래스  
  
|이름|Description|  
|----------|-----------------|  
|public void registerOutParameter (int parameterIndex, int sqlType, int 정밀도, 배율 int)<br /><br /> public void registerOutParameter (int parameterIndex, SQLType sqlType, int 정밀도, 배율 int)<br /><br /> public void registerOutParameter (문자열 parameterName, int sqlType, int 정밀도, 배율 int)<br /><br /> public void registerOutParameter (문자열 parameterName, SQLType sqlType, int 정밀도, 배율 int)<br />public void setBigDecimal (문자열 parameterName, BigDecimal bd, int 정밀도, 배율 int)<br /><br /> public void setTime (문자열 parameterName, java.sql.Time t, int 배율)<br /><br /> public void setTimestamp (문자열 parameterName, t java.sql.Timestamp, int 배율)<br /><br /> public void setDateTimeOffset (parameterName String, microsoft.sql.DateTimeOffset t, int 배율)<br/><br/>공용 최종 void setObject (문자열 sCol, 개체 x, int targetSqlType, 정수 정밀도, 배율 int)|이러한 메서드는 필요한 전체 자릿수 및 소수 자릿수 정보가 특정 데이터 형식에 대 한 상시 암호화를 지원 하기 위해 정밀도 또는 배율 인수 오버 로드 합니다.|  
|public void setDateTime (문자열 parameterName, java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (문자열 parameterName, java.sql.Timestamp x)<br /><br /> public void setUniqueIdentifier (문자열 parameterName, guid 문자열)<br /><br /> public void setMoney (문자열 parameterName, BigDecimal bd)<br /><br /> public void setSmallMoney (문자열 parameterName, BigDecimal bd)<br/><br/>공용 타임 스탬프 getDateTime (int index)<br/><br/>공용 타임 스탬프 getDateTime (문자열 sCol)<br/><br/>공용 타임 스탬프 getDateTime (int 인덱스, 달력 cal)<br/><br/>공용 타임 스탬프 getSmallDateTime (int index)<br/><br/>공용 타임 스탬프 getSmallDateTime (문자열 sCol)<br/><br/>공용 타임 스탬프 getSmallDateTime (int 인덱스, 달력 cal)<br/><br/>공용 타임 스탬프 getSmallDateTime (문자열 이름, 일정 cal)<br/><br/>공용 BigDecimal getMoney (int index)<br/><br/>공용 BigDecimal getMoney (문자열 sCol)<br/><br/>공용 BigDecimal getSmallMoney (int index)<br/><br/>공용 BigDecimal getSmallMoney (문자열 sCol)|이러한 메서드는 데이터 형식 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime에 대 한 상시 암호화를 지원 하기 위해 추가 됩니다. <br/><br/>암호화 된 datetime2 열에 매개 변수 값을 보내는 데 기존 setTimestamp() 메서드를 사용 하는 참고 합니다. 암호화 된 datetime 및 smalldatetime 열에 대 한 각각의 새 메서드 setDateTime() 및 setSmallDateTime() 사용 합니다.|  
|public void setObject (문자열 parameterName, 개체 o, n int, int m, 부울 forceEncrypt)<br /><br /> public void setObject (문자열 parameterName, obj 개체, SQLType jdbcType, int 배율, 부울 forceEncrypt)<br /><br /> public void setDate (문자열 parameterName, x, 달력 c java.sql.Date 부울 forceEncrypt)<br /><br /> public void setTime (문자열 parameterName, java.sql.Time t, int 배율, 부울 forceEncrypt)<br /><br /> public void setTime (문자열 parameterName, x, 달력 c java.sql.Time 부울 forceEncrypt)<br /><br /> public void setDateTime (문자열 parameterName, x, 부울 forceEncrypt java.sql.Timestamp)<br /><br /> public void setDateTimeOffset (parameterName String, microsoft.sql.DateTimeOffset t, int 배율, 부울 forceEncrypt)<br /><br /> public void setSmallDateTime (문자열 parameterName, x, 부울 forceEncrypt java.sql.Timestamp)<br /><br /> public void setTimestamp (문자열 parameterName, t java.sql.Timestamp, int 배율, 부울 forceEncrypt)<br /><br /> public void setTimestamp (문자열 parameterName, x, 부울 forceEncrypt java.sql.Timestamp)<br /><br /> public void setUniqueIdentifier (문자열 parameterName, 문자열 guid, boolean forceEncrypt)<br /><br /> public void setBytes (parameterName 문자열, 바이트 b, 부울 forceEncrypt)<br /><br /> public void setByte (parameterName 문자열, 바이트 b, 부울 forceEncrypt)<br /><br /> public void setString (문자열 parameterName, string, boolean forceEncrypt)<br /><br /> 공용 최종 void setNString (문자열 parameterName, 문자열 값, 부울 forceEncrypt)<br /><br /> public void setMoney (문자열 parameterName, BigDecimal bd, 부울 forceEncrypt)<br /><br /> public void setSmallMoney (문자열 parameterName, BigDecimal bd, 부울 forceEncrypt)<br /><br /> public void setBigDecimal (문자열 parameterName, BigDecimal bd, 전체 자릿수 int, int 배율, 부울 forceEncrypt)<br /><br /> public void setDouble (parameterName 문자열, double d, 부울 forceEncrypt)<br /><br /> public void setFloat (문자열 parameterName, f float, boolean forceEncrypt)<br /><br /> public void setInt (문자열 parameterName, int i, 부울 forceEncrypt)<br /><br /> public void setLong (문자열 parameterName, l long, boolean forceEncrypt)<br /><br /> public void setShort (문자열 parameterName, 짧은 s, 부울 forceEncrypt)<br /><br /> public void setBoolean (문자열 parameterNames, b는 부울 값, 부울 forceEncrypt)<br/><br/>public void setTimeStamp (문자열 sCol, x, 달력 c java.sql.Timestamp 부울 forceEncrypt)|지정된 된 매개 변수를 지정 된 java 값으로 설정합니다.<br /><br /> 부울 forceEncrypt 설정 된 경우 쿼리를 true로 매개 변수는 경우에 설정 지정 열이 암호화 하 고 연결 또는 명령문에 상시 암호화 사용 합니다.<br /><br /> 부울 forceEncrypt가 false로 설정 하는 경우 드라이버는 매개 변수에 대 한 암호화를 요구 하지 않습니다.|
 

 새로 추가 되거나 오버 로드 된 메서드 **SQLServerResultSet** 클래스  
  
|이름|Description|  
|----------|-----------------|  
|공용 문자열 getUniqueIdentifier (int columnIndex)<br/><br/>공용 문자열 getUniqueIdentifier (문자열 columnLabel)<br/><br/>   공용 java.sql.Timestamp getDateTime (int columnIndex) <br/><br/> 공용 java.sql.Timestamp getDateTime (문자열 columnName)   <br/><br/> 공용 java.sql.Timestamp getDateTime (int columnIndex, 달력 cal)   <br/><br/>공용 java.sql.Timestamp getDateTime (문자열 colName, 달력 cal)    <br/><br/>공용 java.sql.Timestamp getSmallDateTime (int columnIndex)    <br/><br/> 공용 java.sql.Timestamp getSmallDateTime (문자열 columnName)   <br/><br/> 공용 java.sql.Timestamp getSmallDateTime (int columnIndex, 달력 cal)   <br/><br/> 공용 java.sql.Timestamp getSmallDateTime (문자열 colName, 달력 cal)   <br/><br/>  공용 BigDecimal getMoney (int columnIndex)  <br/><br/> 공용 BigDecimal getMoney (문자열 columnName)   <br/><br/> 공용 BigDecimal getSmallMoney (int columnIndex)   <br/><br/>  공용 BigDecimal getSmallMoney (문자열 columnName)  <br/><br/>public void updateMoney (문자열 columnName, BigDecimal x)    <br/><br/>  public void updateSmallMoney (문자열 columnName, BigDecimal x)  <br/><br/>     public void updateDateTime (int 인덱스 java.sql.Timestamp x) <br/><br/> public void updateSmallDateTime (int 인덱스 java.sql.Timestamp x) |이러한 메서드는 데이터 형식 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime에 대 한 상시 암호화를 지원 하기 위해 추가 됩니다. <br/><br/>암호화 된 datetime2 열 업데이트에 대 한 기존 updateTimestamp() 메서드를 사용 하는 참고 합니다. 암호화 된 datetime 및 smalldatetime 열에 대 한 각각의 새 메서드 updateDateTime() 및 updateSmallDateTime() 사용 합니다.|
|public void updateBoolean (int 인덱스, 부울 x, 부울 forceEncrypt)  <br/><br/>  public void updateByte (int 인덱스, x, 부울 forceEncrypt byte)  <br/><br/>  public void updateShort (int 인덱스, 짧은 x, 부울 forceEncrypt)  <br/><br/> public void updateInt (int 인덱스, x, 부울 forceEncrypt int)   <br/><br/>  public void updateLong (int 인덱스, x long, boolean forceEncrypt)  <br/><br/> public void updateFloat (int 인덱스, x float, boolean forceEncrypt)   <br/><br/> public void updateDouble (int index, double x, 부울 forceEncrypt)   <br/><br/> public void updateMoney (int index, x, 부울 forceEncrypt BigDecimal)   <br/><br/>  public void updateMoney (문자열 columnName, x, 부울 forceEncrypt BigDecimal)  <br/><br/> public void updateSmallMoney (int index, x, 부울 forceEncrypt BigDecimal)   <br/><br/>  public void updateSmallMoney (문자열 columnName, x, 부울 forceEncrypt BigDecimal)  <br/><br/> public void updateBigDecimal (int 인덱스, x, 정수 정밀도 BigDecimal, 크기 조정 정수, 부울 forceEncrypt)   <br/><br/>  public void updateString (int columnIndex, stringValue 문자열, 부울 forceEncrypt)  <br/><br/>  public void updateNString (int columnIndex, nString 문자열, 부울 forceEncrypt)  <br/><br/>  public void updateNString (문자열 columnLabel, nString 문자열, 부울 forceEncrypt)  <br/><br/> public void updateBytes (int 인덱스, 바이트 x[], 부울 forceEncrypt)   <br/><br/>  public void updateDate (int 인덱스, x, 부울 forceEncrypt java.sql.Date)  <br/><br/> public void updateTime (int 인덱스, x, 정수 배율 java.sql.Time 부울 forceEncrypt)   <br/><br/> public void updateTimestamp (x, int 비율, java.sql.Timestamp, int 인덱스 부울 forceEncrypt)   <br/><br/> public void updateDateTime (x, 정수 비율, java.sql.Timestamp, int 인덱스 부울 forceEncrypt)   <br/><br/> public void updateSmallDateTime (x, 정수 비율, java.sql.Timestamp, int 인덱스 부울 forceEncrypt)   <br/><br/>  public void updateDateTimeOffset (int 인덱스, x, 정수 비율, microsoft.sql.DateTimeOffset 부울 forceEncrypt)  <br/><br/> public void updateUniqueIdentifier (int index, x, 부울 forceEncrypt 문자열)    <br/><br/>  public void updateObject (int 인덱스를 개체 x, int 정밀도, 배율 int, boolean forceEncrypt)  <br/><br/>  public void updateObject (int 인덱스, obj 개체, SQLType targetSqlType, int 배율, 부울 forceEncrypt)  <br/><br/> public void updateBoolean (columnName 문자열, 부울 x, 부울 forceEncrypt)    <br/><br/>  public void updateByte (columnName 문자열, 부울 forceEncrypt x 바이트)  <br/><br/>  public void updateShort (문자열 columnName, 짧은 x, 부울 forceEncrypt)  <br/><br/> public void updateInt (문자열 columnName, x, 부울 forceEncrypt int)   <br/><br/>   public void updateLong (문자열 columnName, x long, boolean forceEncrypt) <br/><br/>  public void updateFloat (문자열 columnName, x float, boolean forceEncrypt)  <br/><br/>  public void updateDouble (columnName 문자열, double x, 부울 forceEncrypt)  <br/><br/> public void updateBigDecimal (문자열 columnName, x, 부울 forceEncrypt BigDecimal)   <br/><br/>  public void updateBigDecimal (x, 정수 정밀도 BigDecimal 문자열 열 이름, 크기 조정 정수, 부울 forceEncrypt)  <br/><br/> public void updateString (문자열 columnName, x, 부울 forceEncrypt 문자열)   <br/><br/>  public void updateBytes (columnName 문자열, 바이트 x[], 부울 forceEncrypt)  <br/><br/> public void updateDate (문자열 columnName, x, 부울 forceEncrypt java.sql.Date)   <br/><br/>  public void updateTime (문자열 columnName, x, int 배율 java.sql.Time 부울 forceEncrypt)  <br/><br/>  public void updateTimestamp (문자열 columnName, x, int 배율 java.sql.Timestamp 부울 forceEncrypt)  <br/><br/> public void updateDateTime (문자열 columnName, x, int 배율 java.sql.Timestamp 부울 forceEncrypt)   <br/><br/>  public void updateSmallDateTime (문자열 columnName, x, int 배율 java.sql.Timestamp 부울 forceEncrypt)  <br/><br/>  public void updateDateTimeOffset (String columnName, x, int 비율, microsoft.sql.DateTimeOffset 부울 forceEncrypt)  <br/><br/>  public void updateUniqueIdentifier (문자열 columnName, x, 부울 forceEncrypt 문자열)<br/><br/>public void updateObject (문자열 열 이름, 개체 x, int 정밀도, 배율 int, boolean forceEncrypt)<br/><br/>public void updateObject (문자열 columnName, obj 개체, SQLType targetSqlType, int 배율, 부울 forceEncrypt)|지정 된 java 값으로 지정된 된 열을 업데이트 합니다.<br/><br/>부울 forceEncrypt로 설정 되어 있으면 true 이면 열은 경우에 설정 암호화 되 고 문이 또는 연결에서 상시 암호화에 사용 됩니다.<br/><br/>부울 forceEncrypt가 false로 설정 하는 경우 드라이버는 매개 변수에 대 한 암호화를 요구 하지 않습니다.|

  
새로운 형식 **microsoft.sql.Types** 클래스
|이름|Description|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|매개 변수 값을 보낼 때 대상 SQL 형식으로 이러한 형식은 사용 하 여 **암호화 된** datetime, smalldatetime, money, smallmoney, setObject()/updateObject() API 메서드를 사용 하 여 uniqueidentifier 열입니다.|  
  
  
 **SQLServerStatementColumnEncryptionSetting 열거형**  
  
 데이터는 전송 및 암호화 된 열을 쓸 때 받은 방법을 지정 합니다. 특정 쿼리에 따라 암호화 되지 않은 열을 사용 하는 경우 항상 암호화 드라이버의 처리를 무시 하 여 성능에 영향을 줄일 수 있습니다. Note 이러한 설정은 암호화를 무시 하 고 일반 텍스트 데이터에 액세스를 사용할 수 없습니다.  
  
 **구문**  
  
```  
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **멤버**  
  
|이름|Description|  
|----------|-----------------|  
|UseConnectionSetting|이 명령은 지정 되도록 지정 연결 문자열에 항상 암호화 설정으로 합니다.|  
|설정|쿼리에 대해 상시 암호화를 사용 합니다.|  
|ResultSetOnly|명령의 결과만 드라이버의 항상 암호화 루틴에 의해 처리 되어야 한다는 것을 지정 합니다. 명령에 암호화를 필요로 하는 매개 변수가 없는 경우에이 값을 사용 합니다.|  
|사용 안 함|쿼리에 대해 상시 암호화를 해제합니다.|  
  
 AE의 문 수준 설정은 SQLServerConnectionPoolProxy 클래스에는 SQLServerConnection 클래스에 추가 됩니다. 이러한 클래스에 다음 메서드는 새 설정으로 오버 로드 합니다.  
  
|이름|Description|  
|----------|-----------------|  
|공용 문 createStatement (int n 유형, nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|지정 된 형식, 동시성, 유지 및 열 암호화 설정으로 결과 집합 개체를 생성 하는 문 개체를 만듭니다.|  
|공용 CallableStatement prepareCall (문자열 sql, int n 유형, nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)|지정 된 형식, 동시성 및 유지 기능을 사용 하 여 결과 집합 개체를 생성 하 고 지정 된 열 암호화 설정으로 CallableStatement 개체를 만듭니다.|  
|공용 PreparedStatement prepareStatement (문자열 sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|자동 생성 키를 검색 하는 기능이 고 지정 된 열 암호화 설정으로 PreparedStatement 개체를 만듭니다.|  
|공용 PreparedStatement prepareStatement (문자열 sql, String columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|지정 된 열 이름 사용 하 여 결과 집합 개체를 생성 하 고 지정 된 열 암호화 설정으로 PreparedStatement 개체를 만듭니다.|  
|공용 PreparedStatement prepareStatement (문자열 sql, int columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting|지정 된 열 인덱스를 사용 하 여 결과 집합 개체를 생성 하 고 지정 된 열 암호화 설정으로 PreparedStatement 개체를 만듭니다.|  
|공용 PreparedStatement prepareStatement (문자열 sql, int n 유형, nConcur int, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|지정 된 형식, 동시성 및 유지 기능을 사용 하 여 결과 집합 개체를 생성 하 고 지정 된 열 암호화 설정으로 PreparedStatement 개체를 만듭니다.|  
  
> [!NOTE]  
>  쿼리에 대해 상시 암호화 사용 하지 않도록 설정 하는 경우 쿼리에 암호화 된 (매개 변수 암호화 된 열에 해당 하는) 해야 하는 매개 변수가 있는 쿼리가 실패 합니다.  
>   
>  쿼리에 대해 상시 암호화 사용 하지 않도록 설정 하는 경우 암호화 된 열에서 결과 반환 하는 쿼리는 쿼리가 암호화 된 값을 반환 합니다. 암호화 된 값 varbinary 데이터 형식을 갖습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [상시 암호화와 JDBC 드라이버 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  
  
