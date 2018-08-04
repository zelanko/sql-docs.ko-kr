---
title: JDBC 드라이버에 대해 Always Encrypted API 참조 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1b720a607b702e93643d70b40a5e6ab036f2f56
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279254"
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>JDBC 드라이버에 대해 Always Encrypted API 참조
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  상시 암호화를 사용하면 클라이언트가 클라이언트 응용 프로그램의 중요한 데이터를 암호화하고 암호화 키를 SQL Server에 표시하지 않을 수 있습니다. 클라이언트 컴퓨터에 설치된 상시 암호화 지원 드라이버가 SQL Server 클라이언트 응용 프로그램의 중요한 데이터를 자동으로 암호화하고 암호 해독하여 이 기능을 구현합니다. 드라이버는 데이터를 SQL Server로 전달하기 전에 중요한 열의 데이터를 암호화하고 응용 프로그램에 대한 의미 체계가 유지되도록 자동으로 쿼리를 다시 작성합니다. 마찬가지로, 드라이버는 쿼리 결과에 있는 암호화된 데이터베이스 열에 저장된 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 하 고 [상시 암호화와 JDBC 드라이버를 사용 하 여](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)입니다.  
  
> [!NOTE]  
>  상시 암호화는 SQL Server용 Microsoft JDBC Driver 6.0 이상과 SQL Server 2016을 함께 사용할 때 지원됩니다.  
  
 ## <a name="always-encrypted-api-references"></a>Always Encrypted API 참조
 
 상시 암호화를 사용하는 클라이언트 응용 프로그램에서 사용하기 위해 JDBC 드라이버 API에 몇 가지 새로운 기능이 추가되고 수정되었습니다.  
  
 **SQLServerConnection 클래스**  
  
|속성|설명|  
|----------|-----------------|  
|새 연결 문자열 키워드:<br /><br /> columnEncryptionSetting|columnEncryptionSetting=Enabled로 설정하면 연결에 대해 상시 암호화 기능이 사용되고 columnEncryptionSetting=Disabled로 설정하면 상시 암호화 기능이 사용되지 않습니다. 허용되는 값이 사용/사용 안 함으로 설정되었습니다. 기본값은 Disabled입니다.|  
|새 메서드:<br /><br /> public static void setColumnEncryptionTrustedMasterKeyPaths (지도 < 문자열, 목록\<문자열 >> trustedKeyPaths)<br /><br /> public static void updateColumnEncryptionTrustedMasterKeyPaths (서버 문자열 목록\<문자열 > trustedKeyPaths)<br /><br /> public static void removeColumnEncryptionTrustedMasterKeyPaths (문자열 server)|데이터베이스 서버에 대해 신뢰할 수 있는 키 경로 목록을 설정/업데이트/제거할 수 있습니다. 응용 프로그램 쿼리를 처리하는 동안 드라이버에서 목록에 없는 키 경로를 수신하면 쿼리가 실패합니다. 이 속성은 손상된 SQL Server가 가짜 키 경로를 보내고 키 저장소 자격 증명을 유출하는 보안 공격에 대한 추가 보호 기능을 제공합니다.|  
|새 메서드:<br /><br /> public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()|데이터베이스 서버에 대한 신뢰할 수 있는 키 경로 목록을 반환합니다.|  
|새 메서드:<br /><br /> public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)|사용자 지정 키 저장소 공급자를 등록할 수 있습니다. 키 저장소 공급자 이름을 키 저장소 공급자 구현에 매핑하는 사전입니다.<br /><br /> JVM 키 저장소를 사용하려면 JVM 키 저장소 자격 증명으로 SQLServerColumnEncryptionJVMKeyStoreProvider 개체를 인스턴스화하고 드라이버에 등록해야 합니다. 이 공급자의 이름은 'MSSQL_JVM_KEYSTORE'여야 합니다.<br /><br /> Azure Key Vault 저장소를 사용 하려면 SQLServerColumnEncryptionAzureKeyStoreProvider 개체를 인스턴스화하고 드라이버를 사용 하 여 등록 해야 합니다. 이 공급자의 이름을 '위해 AZURE_KEY_VAULT' 이어야 합니다.|
|public final boolean getSendTimeAsDatetime()|SendTimeAsDatetime 연결 속성의 설정을 반환 합니다.|
|public void setSendTimeAsDatetime (부울 sendTimeAsDateTimeValue)|SendTimeAsDatetime 연결 속성의 설정을 수정합니다.|

 **SQLServerConnectionPoolProxy 클래스**
|속성|설명|  
|----------|-----------------|  
|public final boolean getSendTimeAsDatetime()|SendTimeAsDatetime 연결 속성의 설정을 반환 합니다.|
|public void setSendTimeAsDatetime (부울 sendTimeAsDateTimeValue)|SendTimeAsDatetime 연결 속성의 설정을 수정합니다.|
     
  
 **SQLServerDataSource 클래스**  
  
|속성|설명|  
|----------|-----------------|  
|public void setColumnEncryptionSetting(String columnEncryptionSetting)|데이터 원본 개체에 대해 상시 암호화 기능을 사용하거나 사용하지 않습니다.<br /><br /> 기본값은 Disabled입니다.|  
|공개 문자열 getColumnEncryptionSetting()|데이터 원본 개체에 대한 상시 암호화 기능 설정을 가져옵니다.|
|public void setKeyStoreAuthentication (문자열 keyStoreAuthentication)|키 저장소를 식별하는 이름을 설정합니다. 지원 되는 값만이 **JavaKeyStorePassword** Java 키 저장소를 식별 하는 데 있습니다.<br/><br/>기본값은 null입니다.|
|공개 문자열 getKeyStoreAuthentication()|데이터 원본 개체에 대 한 keyStoreAuthentication 설정의 값을 가져옵니다.|
|public void setKeyStoreSecret (문자열 keyStoreSecret)|Java 키 저장소에 대 한 암호를 설정합니다. 키 저장소 및 키에 대 한 암호는 같아야 합니다. 사용 하 여 설정 해야 해당 keyStoreAuthentication **JavaKeyStorePassword**합니다.|
|public void setKeyStoreLocation (문자열 keyStoreLocation)|Java 키 저장소 파일 이름을 포함 한 위치를 설정 합니다. 사용 하 여 설정 해야 해당 keyStoreAuthentication **JavaKeyStorePassword**합니다.|
|공개 문자열 getKeyStoreLocation()|Java 키 저장소 용 keyStoreLocation를 검색합니다.|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 클래스**  
  
 Java 키 저장소에 대한 키 저장소 공급자의 구현입니다. 이 클래스를 사용하면 Java 키 저장소에 저장된 인증서를 열 마스터 키로 사용할 수 있습니다.  
  
 생성자  
  
|속성|설명|  
|----------|-----------------|  
|공용 SQLServerColumnEncryptionJavaKeyStoreProvider (문자열 keyStoreLocation, char keyStoreSecret)|Java 키 저장소에 대 한 키 저장소 공급자입니다.|  
  
 메서드  
  
|속성|설명|  
|----------|-----------------|  
|public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)|열 암호화 키의 지정된 암호화 값을 암호 해독합니다. 암호화 값은 지정된 키 경로가 있는 인증서와 지정된 알고리즘을 사용하여 암호화해야 합니다.<br /><br /> **키 경로 형식은 다음 중 하나여야 합니다.**<br /><br /> 지문:<certificate_thumbprint><br /><br /> 별칭:<certificate_alias><br /><br /> (SQLServerColumnEncryptionKeyStoreProvider를 재정의합니다. (String, String, Byte[]).) decryptColumnEncryptionKey|  
|public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)|지정된 키 경로가 있는 인증서와 지정된 알고리즘을 사용하여 열 암호화 키를 암호화합니다.<br /><br /> **키 경로 형식은 다음 중 하나여야 합니다.**<br /><br /> 지문:<certificate_thumbprint><br /><br /> 별칭:<certificate_alias><br /><br /> (SQLServerColumnEncryptionKeyStoreProvider를 재정의합니다. (String, String, Byte[]).) encryptColumnEncryptionKey|  
|public void setName (문자열 이름)|이 키 저장소 공급자의 이름을 설정합니다.|
|public String getName()|이 키 저장소 공급자의 이름을 가져옵니다.|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 클래스**  
  
 Azure Key Vault 저장소에 대한 키 저장소 공급자의 구현입니다. 이 클래스는 열 마스터 키로 Azure Key Vault에 저장 된 키를 사용할 수 있습니다.  
  
 생성자  
  
|속성|설명|  
|----------|-----------------|  
|공용 SQLServerColumnEncryptionAzureKeyVaultProvider (String clientId, 문자열 clientKey)|Azure Key Vault에 대 한 키 저장소 공급자입니다.  식별자 및 Azure Key Vault에 인증 토큰을 요청 클라이언트의 키를 제공 해야 합니다.|  
  
 메서드  
  
|속성|설명|  
|----------|-----------------|  
|public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)|열 암호화 키의 지정된 암호화 값을 암호 해독합니다. 암호화된 값은 지정된 열 키 IDmaster 키를 사용하고 지정된 알고리즘을 사용하여 암호화해야 합니다. <br />(SQLServerColumnEncryptionKeyStoreProvider를 재정의합니다. (String, String, Byte[]).) decryptColumnEncryptionKey|  
|public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)|지정 된 열 마스터 키를 사용 하 고 지정된 된 알고리즘을 사용 하 여 열 암호화 키를 암호화 합니다. <br />(SQLServerColumnEncryptionKeyStoreProvider를 재정의합니다. (String, String, Byte[]).) encryptColumnEncryptionKey|  
|public void setName (문자열 이름)|이 키 저장소 공급자의 이름을 설정합니다.|
|public String getName()|이 키 저장소 공급자의 이름을 가져옵니다.|  
  
  
 **SQLServerKeyVaultAuthenticationCallback 인터페이스**  
  
 이 인터페이스는 사용자가 구현 하는 Azure Key Vault 인증에 대 한 하나의 메서드를 포함 합니다.  
  
 메서드  
  
|속성|설명|  
|----------|-----------------|  
|공개 문자열 getAccessToken (권한 문자열, 문자열 리소스, 문자열 범위).|메서드를 재정의 해야 합니다. 메서드는 토큰을 가져오는 액세스 Azure Key Vault에 사용 됩니다.|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 클래스**  
  
 사용자 지정 키 저장소 공급자를 구현하려면 이 클래스를 확장합니다.  
  
|속성|설명|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|모든 키 저장소 공급자에 대한 기본 클래스입니다. 사용자 지정 공급자는 이 클래스에서 파생되어 해당 멤버 함수를 재정의한 다음, SQLServerConnection을 사용하여 등록해야 합니다. registerColumnEncryptionKeyStoreProviders() 합니다.|  
  
 메서드  
  
|속성|설명|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|열 암호화 키의 지정된 암호화 값을 암호 해독하는 기본 클래스 메서드입니다. 암호화된 값은 지정된 키 경로와 지정된 알고리즘이 있는 열 마스터 키를 사용하여 암호화해야 합니다.|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|지정된 키 경로가 있는 열 마스터 키와 지정된 알고리즘을 사용하여 열 암호화 키를 암호화하기 위한 기본 클래스 메서드입니다.|
|공용 추상 void setName (문자열 이름)|이 키 저장소 공급자의 이름을 설정합니다.|
|공용 추상 문자열 getName()|이 키 저장소 공급자의 이름을 가져옵니다.|  
  
 새 또는 오버 로드 된 메서드 **SQLServerPreparedStatement** 클래스  
  
|속성|설명|  
|----------|-----------------|  
|public void setBigDecimal (int 된, x, int 정밀도 BigDecimal int 확장)<br /><br /> public void setObject (int 된, 개체 x, int targetSqlType int 크기 조정 정수 전체 자릿수)<br /><br /> public void setObject (int 된, 개체 x, SQLType targetSqlType 정수 크기 조정 정수 전체 자릿수)<br /><br /> public void setTime (int 된, x, int 확장 java.sql.Time)<br /><br /> public void setTimestamp (int 된, x, int 확장 java.sql.Timestamp) <br />public void setDateTimeOffset (int 된, x, int 확장 microsoft.sql.DateTimeOffset)|필요한 전체 자릿수 및 소수 자릿수 정보가 특정 데이터 형식에 대 한 Always Encrypted를 지원 하기 위해 정밀도 또는 배율 인수를 사용 하 여 이러한 메서드 오버 로드 됩니다.|  
|public void setMoney (int 된, BigDecimal x)<br /><br /> public void setSmallMoney (int 된, BigDecimal x)<br /><br /> public void setUniqueIdentifier (int 된, guid 문자열)<br /><br /> public void setDateTime (int 된 java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (int 된 java.sql.Timestamp x)|이러한 메서드는 데이터 형식 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime에 대 한 Always Encrypted를 지원 하기 위해 추가 됩니다. <br/><br/>암호화 된 datetime2 열에 매개 변수 값을 전송 하는 것에 대 한 기존 setTimestamp() 메서드를 사용 하는 참고 합니다. 암호화 된 datetime 및 smalldatetime 열에 대 한 각각의 새 메서드 setDateTime() 및 setSmallDateTime() 사용 합니다.|  
|공용 최종 void setBigDecimal (int 된, x, int 정밀도 BigDecimal, int 크기 조정, 부울 forceEncrypt)<br /><br /> 공용 최종 void setMoney (int 된, x, 부울 forceEncrypt BigDecimal)<br /><br /> 공용 최종 void setSmallMoney (int 된, x, 부울 forceEncrypt BigDecimal)<br /><br /> 공용 최종 void setBoolean (int 된, 부울 x, 부울 forceEncrypt)<br /><br /> 공용 최종 void setByte (int 된, x, 부울 forceEncrypt byte)<br /><br /> 공용 최종 void setBytes (int 된, 바이트 x[] 부울 forceEncrypt)<br /><br /> 공용 최종 void setUniqueIdentifier (int 된, guid 문자열, 부울 forceEncrypt)<br /><br /> 공용 최종 void setDouble (int 된 double x, 부울 forceEncrypt)<br /><br /> 공용 최종 void setFloat (된 int, float x, 부울 forceEncrypt)<br /><br /> 공용 최종 void setInt (된 int, int 값, 부울 forceEncrypt)<br /><br /> 공용 최종 void setLong (int 된, 장기 x, 부울 forceEncrypt)<br /><br /> 공용 최종 setObject (int 된, 개체 x, int targetSqlType, 정수 전체 자릿수, 소수 int 부울 forceEncrypt)<br /><br /> 공용 최종 void setObject (int 된, 개체 x, SQLType targetSqlType, 정수 전체 자릿수, 크기 조정 정수, 부울 forceEncrypt)<br /><br /> 공용 최종 void setShort (된 int, short x, 부울 forceEncrypt)<br /><br /> 공용 최종 void setString (int 된, str 문자열, 부울 forceEncrypt)<br /><br /> 공용 최종 void setNString (int 된, 문자열 값, 부울 forceEncrypt)<br /><br /> 공용 최종 void setTime (int 된, x, int 확장 java.sql.Time 부울 forceEncrypt)<br /><br /> 공용 최종 void setTimestamp (x, int 비율, java.sql.Timestamp, int 된 부울 forceEncrypt)<br /><br /> 공용 최종 void setDateTimeOffset (int 된, x, int 확장 microsoft.sql.DateTimeOffset 부울 forceEncrypt)<br /><br /> 공용 최종 void setDateTime (된 int, java.sql.Timestamp 부울 forceEncrypt x)<br /><br /> 공용 최종 void setSmallDateTime (된 int, java.sql.Timestamp 부울 forceEncrypt x)<br /><br /> 공용 최종 void setDate (int 된, java.sql.Date, java.util.Calendar cal x 부울 forceEncrypt)<br /><br /> 공용 최종 void setTime (int 된, java.sql.Time, java.util.Calendar cal x 부울 forceEncrypt)<br /><br /> 공용 최종 void setTimestamp (int 된, java.sql.Timestamp, java.util.Calendar cal x 부울 forceEncrypt)|지정된 매개 변수를 지정된 java 값으로 설정합니다.<br /><br /> 부울 forceEncrypt 설정 되어 있으면 true, 쿼리를 매개 변수는 경우에 설정 지정 열 암호화 되 고 연결 또는 문이 상시 암호화 사용 합니다.<br /><br /> 부울 forceEncrypt가 false로 설정 하는 경우 드라이버 매개 변수에 대해 암호화를 강제 하지 않습니다.|  
  
 새 또는 오버 로드 된 메서드 **SQLServerCallableStatement** 클래스  
  
|속성|설명|  
|----------|-----------------|  
|public void registerOutParameter (int 된, sqlType int, int 정밀도, int 확장)<br /><br /> public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)<br /><br /> public void registerOutParameter (문자열 parameterName, sqlType int, int 정밀도, int 확장)<br /><br /> public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)<br />public void setBigDecimal (문자열 parameterName, BigDecimal bd, 정밀도 int, int 확장)<br /><br /> public void setTime (문자열 parameterName, java.sql.Time t, int 소수 자릿수)<br /><br /> public void setTimestamp (문자열 parameterName, t java.sql.Timestamp, int 소수 자릿수)<br /><br /> public void setDateTimeOffset (문자열 parameterName, microsoft.sql.DateTimeOffset t, int 소수 자릿수)<br/><br/>공용 최종 void setObject (sCol 문자열, 개체 x, int targetSqlType int 크기 조정 정수 전체 자릿수)|필요한 전체 자릿수 및 소수 자릿수 정보가 특정 데이터 형식에 대 한 Always Encrypted를 지원 하기 위해 정밀도 또는 배율 인수를 사용 하 여 이러한 메서드 오버 로드 됩니다.|  
|public void setDateTime (문자열 parameterName, java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (문자열 parameterName, java.sql.Timestamp x)<br /><br /> public void setUniqueIdentifier (parameterName 문자열, 문자열 guid)<br /><br /> public void setMoney (문자열 parameterName, BigDecimal bd)<br /><br /> public void setSmallMoney (문자열 parameterName, BigDecimal bd)<br/><br/>공용 타임 스탬프 getDateTime (int 인덱스)<br/><br/>공용 타임 스탬프 getDateTime (문자열 sCol)<br/><br/>공용 타임 스탬프 getDateTime (int 인덱스, 달력 cal)<br/><br/>공용 타임 스탬프 getSmallDateTime (int 인덱스)<br/><br/>공용 타임 스탬프 getSmallDateTime (문자열 sCol)<br/><br/>공용 타임 스탬프 getSmallDateTime (int 인덱스, 달력 cal)<br/><br/>공용 타임 스탬프 getSmallDateTime (문자열 이름, 일정 cal)<br/><br/>공용 BigDecimal getMoney (int 인덱스)<br/><br/>공용 BigDecimal getMoney (문자열 sCol)<br/><br/>공용 BigDecimal getSmallMoney (int 인덱스)<br/><br/>공용 BigDecimal getSmallMoney (문자열 sCol)|이러한 메서드는 데이터 형식 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime에 대 한 Always Encrypted를 지원 하기 위해 추가 됩니다. <br/><br/>암호화 된 datetime2 열에 매개 변수 값을 전송 하는 것에 대 한 기존 setTimestamp() 메서드를 사용 하는 참고 합니다. 암호화 된 datetime 및 smalldatetime 열에 대 한 각각의 새 메서드 setDateTime() 및 setSmallDateTime() 사용 합니다.|  
|public void setObject (문자열 parameterName, 개체 o, n int, int m, 부울 forceEncrypt)<br /><br /> public void setObject (문자열 parameterName, 개체 obj, SQLType jdbcType, int 크기 조정, 부울 forceEncrypt)<br /><br /> public void setDate (문자열 parameterName, x, 달력 c java.sql.Date 부울 forceEncrypt)<br /><br /> public void setTime (문자열 parameterName, java.sql.Time t, int 크기 조정, 부울 forceEncrypt)<br /><br /> public void setTime (문자열 parameterName, x, 달력 c java.sql.Time 부울 forceEncrypt)<br /><br /> public void setDateTime (문자열 parameterName, x, 부울 forceEncrypt java.sql.Timestamp)<br /><br /> public void setDateTimeOffset (문자열 parameterName, microsoft.sql.DateTimeOffset t, int 확장, 부울 forceEncrypt)<br /><br /> public void setSmallDateTime (문자열 parameterName, x, 부울 forceEncrypt java.sql.Timestamp)<br /><br /> public void setTimestamp (문자열 parameterName, t java.sql.Timestamp, int 확장, 부울 forceEncrypt)<br /><br /> public void setTimestamp (문자열 parameterName, x, 부울 forceEncrypt java.sql.Timestamp)<br /><br /> public void setUniqueIdentifier (문자열 parameterName, guid 문자열, 부울 forceEncrypt)<br /><br /> public void setBytes (parameterName 문자열, byte b, 부울 forceEncrypt)<br /><br /> public void setByte (parameterName 문자열, 바이트 b, 부울 forceEncrypt)<br /><br /> public void setString (문자열 parameterName, string, boolean forceEncrypt)<br /><br /> 공용 최종 void setNString (parameterName 문자열, 문자열 값, 부울 forceEncrypt)<br /><br /> public void setMoney (문자열 parameterName, BigDecimal bd, 부울 forceEncrypt)<br /><br /> public void setSmallMoney (문자열 parameterName, BigDecimal bd, 부울 forceEncrypt)<br /><br /> public void setBigDecimal (문자열 parameterName, BigDecimal bd, 전체 자릿수 int, int 확장, 부울 forceEncrypt)<br /><br /> public void setDouble (문자열 parameterName double d, 부울 forceEncrypt)<br /><br /> public void setFloat (문자열 parameterName, f float, boolean forceEncrypt)<br /><br /> public void setInt (parameterName 문자열, int i, 부울 forceEncrypt)<br /><br /> public void setLong (문자열 parameterName, 장기 l, 부울 forceEncrypt)<br /><br /> public void setShort (문자열 parameterName, 단기 s, 부울 forceEncrypt)<br /><br /> public void setBoolean (parameterNames 문자열, 부울 b, 부울 forceEncrypt)<br/><br/>public void setTimeStamp (문자열 sCol, x, 달력 c java.sql.Timestamp 부울 forceEncrypt)|지정된 매개 변수를 지정된 java 값으로 설정합니다.<br /><br /> 부울 forceEncrypt 설정 되어 있으면 true, 쿼리를 매개 변수는 경우에 설정 지정 열 암호화 되 고 연결 또는 문이 상시 암호화 사용 합니다.<br /><br /> 부울 forceEncrypt가 false로 설정 하는 경우 드라이버 매개 변수에 대해 암호화를 강제 하지 않습니다.|
 

 새 또는 오버 로드 된 메서드 **SQLServerResultSet** 클래스  
  
|속성|설명|  
|----------|-----------------|  
|공개 문자열 getUniqueIdentifier (int columnIndex)<br/><br/>공개 문자열 getUniqueIdentifier (문자열 columnLabel)<br/><br/>   공용 java.sql.Timestamp getDateTime (int columnIndex) <br/><br/> 공용 java.sql.Timestamp getDateTime (문자열 columnName)   <br/><br/> 공용 java.sql.Timestamp getDateTime (int columnIndex, 달력 cal)   <br/><br/>공용 java.sql.Timestamp getDateTime (문자열 colName, 달력 cal)    <br/><br/>공용 java.sql.Timestamp getSmallDateTime (int columnIndex)    <br/><br/> 공용 java.sql.Timestamp getSmallDateTime (문자열 columnName)   <br/><br/> 공용 java.sql.Timestamp getSmallDateTime (int columnIndex, 달력 cal)   <br/><br/> 공용 java.sql.Timestamp getSmallDateTime (문자열 colName, 달력 cal)   <br/><br/>  공용 BigDecimal getMoney (int columnIndex)  <br/><br/> 공용 BigDecimal getMoney (문자열 columnName)   <br/><br/> 공용 BigDecimal getSmallMoney (int columnIndex)   <br/><br/>  공용 BigDecimal getSmallMoney (문자열 columnName)  <br/><br/>public void updateMoney (문자열 columnName, BigDecimal x)    <br/><br/>  public void updateSmallMoney (문자열 columnName, BigDecimal x)  <br/><br/>     public void updateDateTime (인덱스 int, java.sql.Timestamp x) <br/><br/> public void updateSmallDateTime (인덱스 int, java.sql.Timestamp x) |이러한 메서드는 데이터 형식 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime에 대 한 Always Encrypted를 지원 하기 위해 추가 됩니다. <br/><br/>암호화 된 datetime2 열을 업데이트 하는 것에 대 한 기존 updateTimestamp() 메서드를 사용 하는 참고 합니다. 암호화 된 datetime 및 smalldatetime 열에 대 한 각각의 새 메서드 updateDateTime() 및 updateSmallDateTime() 사용 합니다.|
|public void updateBoolean (int 인덱스, 부울 x, 부울 forceEncrypt)  <br/><br/>  public void updateByte (int 인덱스, x, 부울 forceEncrypt 바이트)  <br/><br/>  public void updateShort (int 인덱스, 짧은 x, 부울 forceEncrypt)  <br/><br/> public void updateInt (int 인덱스, x, 부울 forceEncrypt int)   <br/><br/>  public void updateLong (int 인덱스, 장기 x, 부울 forceEncrypt)  <br/><br/> public void updateFloat (int 인덱스, x float, boolean forceEncrypt)   <br/><br/> public void updateDouble (int index, double x, 부울 forceEncrypt)   <br/><br/> public void updateMoney (int index, x, 부울 forceEncrypt BigDecimal)   <br/><br/>  public void updateMoney (문자열 columnName, x, 부울 forceEncrypt BigDecimal)  <br/><br/> public void updateSmallMoney (int index, x, 부울 forceEncrypt BigDecimal)   <br/><br/>  public void updateSmallMoney (문자열 columnName, x, 부울 forceEncrypt BigDecimal)  <br/><br/> public void updateBigDecimal (int 인덱스, x, 정수 자릿수 BigDecimal, 크기 조정 정수, 부울 forceEncrypt)   <br/><br/>  public void updateString (int columnIndex, stringValue 문자열, 부울 forceEncrypt)  <br/><br/>  public void updateNString (int columnIndex, 항목이 문자열, 부울 forceEncrypt)  <br/><br/>  public void updateNString (문자열 columnLabel, 항목이 문자열, 부울 forceEncrypt)  <br/><br/> public void updateBytes (int 인덱스, 바이트 x[] 부울 forceEncrypt)   <br/><br/>  public void updateDate (int 인덱스, x, 부울 forceEncrypt java.sql.Date)  <br/><br/> public void updateTime (int 인덱스, x, 정수 확장 java.sql.Time 부울 forceEncrypt)   <br/><br/> public void updateTimestamp (int 인덱스, x, int 확장 java.sql.Timestamp 부울 forceEncrypt)   <br/><br/> public void updateDateTime (인덱스 int x, 정수 확장 java.sql.Timestamp 부울 forceEncrypt)   <br/><br/> public void updateSmallDateTime (인덱스 int x, 정수 확장 java.sql.Timestamp 부울 forceEncrypt)   <br/><br/>  public void updateDateTimeOffset (int 인덱스, x, 정수 확장 microsoft.sql.DateTimeOffset 부울 forceEncrypt)  <br/><br/> public void updateUniqueIdentifier (int index, x, 부울 forceEncrypt 문자열)    <br/><br/>  public void updateObject (int 인덱스 개체 x, int 정밀도, int 크기 조정, 부울 forceEncrypt)  <br/><br/>  공용 void updateObject (int index, 개체 obj, SQLType targetSqlType, int 크기 조정, 부울 forceEncrypt)  <br/><br/> public void updateBoolean (columnName 문자열, 부울 x, 부울 forceEncrypt)    <br/><br/>  public void updateByte (문자열 columnName, x, 부울 forceEncrypt 바이트)  <br/><br/>  public void updateShort (문자열 columnName, 짧은 x, 부울 forceEncrypt)  <br/><br/> public void updateInt (문자열 columnName, x, 부울 forceEncrypt int)   <br/><br/>   public void updateLong (문자열 columnName, 장기 x, 부울 forceEncrypt) <br/><br/>  public void updateFloat (문자열 columnName, x float, boolean forceEncrypt)  <br/><br/>  public void updateDouble (columnName 문자열, double x, 부울 forceEncrypt)  <br/><br/> public void updateBigDecimal (문자열 columnName, x, 부울 forceEncrypt BigDecimal)   <br/><br/>  public void updateBigDecimal (columnName 문자열, 정수 자릿수 x BigDecimal, 크기 조정 정수, 부울 forceEncrypt)  <br/><br/> public void updateString (columnName 문자열, 문자열, 부울 forceEncrypt x)   <br/><br/>  public void updateBytes (columnName 문자열, 바이트 x[] 부울 forceEncrypt)  <br/><br/> public void updateDate (문자열 columnName, x, 부울 forceEncrypt java.sql.Date)   <br/><br/>  public void updateTime (문자열 columnName, x, int 확장 java.sql.Time 부울 forceEncrypt)  <br/><br/>  public void updateTimestamp (문자열 columnName, x, int 확장 java.sql.Timestamp 부울 forceEncrypt)  <br/><br/> public void updateDateTime (문자열 columnName, x, int 확장 java.sql.Timestamp 부울 forceEncrypt)   <br/><br/>  public void updateSmallDateTime (문자열 columnName, x, int 확장 java.sql.Timestamp 부울 forceEncrypt)  <br/><br/>  public void updateDateTimeOffset (String columnName, x, int 확장 microsoft.sql.DateTimeOffset 부울 forceEncrypt)  <br/><br/>  public void updateUniqueIdentifier (columnName 문자열, 문자열, 부울 forceEncrypt x)<br/><br/>public void updateObject (columnName 문자열, 개체 x, 전체 자릿수 int, int 크기 조정, 부울 forceEncrypt)<br/><br/>공용 void updateObject (columnName 문자열, 개체 obj, SQLType targetSqlType, int 크기 조정, 부울 forceEncrypt)|지정 된 java 값으로 지정된 된 열을 업데이트 합니다.<br/><br/>부울 forceEncrypt로 설정 되어 있으면 true 이면 열만 설정 됩니다는 암호화 되 고 연결 또는 문이 상시 암호화 사용 합니다.<br/><br/>부울 forceEncrypt가 false로 설정 하는 경우 드라이버 매개 변수에 대해 암호화를 강제 하지 않습니다.|

  
새 종류 **microsoft.sql.Types** 클래스
|속성|설명|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|매개 변수 값을 보낼 때 이러한 형식을 대상 SQL 형식으로 사용할 **암호화 된** datetime, smalldatetime, money, smallmoney, setObject()/updateObject() API 메서드를 사용 하 여 uniqueidentifier 열입니다.|  
  
  
 **Sqlserverstatementcolumnencryptionsetting은 열거형**  
  
 데이터는 전송 및 암호화 된 열을 쓰고 읽을 때 수신 하는 방법을 지정 합니다. 특정 쿼리에 따라 암호화 되지 않은 열을 사용 하는 경우 상시 암호화 드라이버의 처리를 무시 하 여 성능에 미치는 영향을 줄일 수 있습니다. 암호화를 무시 하 고 일반 텍스트 데이터에 액세스 하려면 이러한 설정을 사용할 수 없음을 note 합니다.  
  
 **구문**  
  
```java
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **멤버**  
  
|속성|설명|  
|----------|-----------------|  
|UseConnectionSetting|명령은 연결 문자열에서 상시 암호화 설정의 기본값은 지정 합니다.|  
|설정|쿼리에 대해 상시 암호화를 사용 합니다.|  
|ResultSetOnly|명령의 결과만 드라이버의 항상 암호화 루틴에 의해 처리 되어야 한다는 것을 지정 합니다. 명령에 암호화가 필요한 매개 변수가 없는 경우이 값을 사용 합니다.|  
|사용 안 함|쿼리에 대해 상시 암호화를 해제합니다.|  
  
 AE의 문 수준 설정은 SQLServerConnectionPoolProxy 클래스 SQLServerConnection 클래스에 추가 됩니다. 새 설정과 이러한 클래스의 다음 메서드를 오버 로드 됩니다.  
  
|속성|설명|  
|----------|-----------------|  
|공용 문 createStatement (int n 형식, nConcur int, int statementHoldability, sqlserverstatementcolumnencryptionsetting은 stmtColEncSetting)|지정 된 형식, 동시성, 유지 기능 및 열 암호화 설정을 사용 하 여 결과 집합 개체를 생성 하는 문 개체를 만듭니다.|  
|공용 CallableStatement prepareCall (sql 문자열, int n 형식, nConcur int, int statementHoldability, sqlserverstatementcolumnencryptionsetting은 stmtColEncSetiing)|지정 된 형식, 동시성 및 유지 기능을 사용 하 여 결과 집합 개체를 생성 하는 지정 된 열 암호화 설정을 사용 하 여 CallableStatement 개체를 만듭니다.|  
|공용 PreparedStatement prepareStatement (sql 문자열, int autogeneratedKeys sqlserverstatementcolumnencryptionsetting은 stmtColEncSetting)|자동 생성 키를 검색 하는 기능에는 지정 된 열 암호화 설정을 사용 하 여 PreparedStatement 개체를 만듭니다.|  
|공용 PreparedStatement prepareStatement (sql 문자열, 문자열 columnNames sqlserverstatementcolumnencryptionsetting은 stmtColEncSetting)|지정 된 열 이름 사용 하 여 결과 집합 개체를 생성 하는 지정 된 열 암호화 설정을 사용 하 여 PreparedStatement 개체를 만듭니다.|  
|공용 PreparedStatement prepareStatement (sql 문자열, int columnIndexes, sqlserverstatementcolumnencryptionsetting은 stmtColEncSetting|지정 된 열 인덱스를 사용 하 여 결과 집합 개체를 생성 하는 지정 된 열 암호화 설정을 사용 하 여 PreparedStatement 개체를 만듭니다.|  
|공용 PreparedStatement prepareStatement (sql 문자열, int n 형식, nConcur int, int nHold, sqlserverstatementcolumnencryptionsetting은 stmtColEncSetting)|지정 된 형식, 동시성 및 유지 기능을 사용 하 여 결과 집합 개체를 생성 하는 지정 된 열 암호화 설정을 사용 하 여 PreparedStatement 개체를 만듭니다.|  
  
> [!NOTE]  
>  쿼리에 대해 상시 암호화 사용 하지 않도록 설정 하 고 쿼리에 암호화 된 (매개 변수 암호화 된 열에 해당 하는) 해야 하는 매개 변수가 있는 경우 쿼리가 실패 합니다.  
>   
>  쿼리에 대해 상시 암호화 사용 하지 않도록 설정 하는 경우 암호화 된 열에서 결과 반환 하는 쿼리는 쿼리가 암호화 된 값을 반환 합니다. 암호화 된 값에는 varbinary 데이터 형식을 갖습니다.  
  
 ## <a name="see-also"></a>참고 항목  
 [상시 암호화와 JDBC 드라이버 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

