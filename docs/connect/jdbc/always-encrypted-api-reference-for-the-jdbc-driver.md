---
title: JDBC 드라이버에 대해 Always Encrypted API 참조 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79cf8ce1b951621d58105d18b847306ff620d114
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028482"
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>JDBC 드라이버에 대해 Always Encrypted API 참조
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  상시 암호화를 사용하면 클라이언트가 클라이언트 애플리케이션의 중요한 데이터를 암호화하고 암호화 키를 SQL Server에 표시하지 않을 수 있습니다. 클라이언트 컴퓨터에 설치된 상시 암호화 지원 드라이버가 SQL Server 클라이언트 애플리케이션의 중요한 데이터를 자동으로 암호화하고 암호 해독하여 이 기능을 구현합니다. 드라이버는 데이터를 SQL Server로 전달하기 전에 중요한 열의 데이터를 암호화하고 애플리케이션에 대한 의미 체계가 유지되도록 자동으로 쿼리를 다시 작성합니다. 마찬가지로, 드라이버는 쿼리 결과에 있는 암호화된 데이터베이스 열에 저장된 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [Always Encrypted (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 [JDBC 드라이버에서 Always Encrypted 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)을 참조 하세요.  
  
> [!NOTE]  
>  상시 암호화는 SQL Server용 Microsoft JDBC Driver 6.0 이상과 SQL Server 2016을 함께 사용할 때 지원됩니다.  
  
 ## <a name="always-encrypted-api-references"></a>Always Encrypted API 참조
 
 상시 암호화를 사용하는 클라이언트 애플리케이션에서 사용하기 위해 JDBC 드라이버 API에 몇 가지 새로운 기능이 추가되고 수정되었습니다.  
  
 **SQLServerConnection 클래스**  
  
|속성|설명|  
|----------|-----------------|  
|새 연결 문자열 키워드:<br /><br /> columnEncryptionSetting|columnEncryptionSetting=Enabled로 설정하면 연결에 대해 상시 암호화 기능이 사용되고 columnEncryptionSetting=Disabled로 설정하면 상시 암호화 기능이 사용되지 않습니다. 허용되는 값이 사용/사용 안 함으로 설정되었습니다. 기본값은 Disabled입니다.|  
|새 메서드:<br /><br /> `public static void setColumnEncryptionTrustedMasterKeyPaths(Map<String, List\<String>> trustedKeyPaths)`<br /><br /> `public static void updateColumnEncryptionTrustedMasterKeyPaths(String server, List\<String> trustedKeyPaths)`<br /><br /> `public static void removeColumnEncryptionTrustedMasterKeyPaths(String server)`|데이터베이스 서버에 대해 신뢰할 수 있는 키 경로 목록을 설정/업데이트/제거할 수 있습니다. 애플리케이션 쿼리를 처리하는 동안 드라이버에서 목록에 없는 키 경로를 수신하면 쿼리가 실패합니다. 이 속성은 손상된 SQL Server가 가짜 키 경로를 보내고 키 저장소 자격 증명을 유출하는 보안 공격에 대한 추가 보호 기능을 제공합니다.|  
|새 메서드:<br /><br /> `public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()`|데이터베이스 서버에 대한 신뢰할 수 있는 키 경로 목록을 반환합니다.|  
|새 메서드:<br /><br /> `public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)`|사용자 지정 키 저장소 공급자를 등록할 수 있습니다. 키 저장소 공급자 이름을 키 저장소 공급자 구현에 매핑하는 사전입니다.<br /><br /> JVM 키 저장소를 사용하려면 JVM 키 저장소 자격 증명으로 SQLServerColumnEncryptionJVMKeyStoreProvider 개체를 인스턴스화하고 드라이버에 등록해야 합니다. 이 공급자의 이름은 'MSSQL_JVM_KEYSTORE'여야 합니다.<br /><br /> Azure Key Vault 저장소를 사용 하려면 SQLServerColumnEncryptionAzureKeyStoreProvider 개체를 인스턴스화하고 드라이버에 등록 해야 합니다. 이 공급자의 이름은 ' AZURE_KEY_VAULT ' 여야 합니다.|
|`public final boolean getSendTimeAsDatetime()`|SendTimeAsDatetime connection 속성의 설정을 반환 합니다.|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)`|SendTimeAsDatetime connection 속성의 설정을 수정 합니다.|

 **SQLServerConnectionPoolProxy 클래스**
 
|속성|설명|  
|----------|-----------------|  
|`public final boolean getSendTimeAsDatetime()` | SendTimeAsDatetime connection 속성의 설정을 반환 합니다.|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)` | SendTimeAsDatetime connection 속성의 설정을 수정 합니다.|
     
  
 **SQLServerDataSource 클래스**  
  
|속성|설명|  
|----------|-----------------|  
|`public void setColumnEncryptionSetting(String columnEncryptionSetting)`|데이터 원본 개체에 대해 상시 암호화 기능을 사용하거나 사용하지 않습니다.<br /><br /> 기본값은 Disabled입니다.|  
|`public String getColumnEncryptionSetting()`|데이터 원본 개체에 대한 상시 암호화 기능 설정을 가져옵니다.|
|`public void setKeyStoreAuthentication(String keyStoreAuthentication)`|키 저장소를 식별하는 이름을 설정합니다. 지원 되는 값만 Java 키 저장소를 식별 하는 **JavaKeyStorePassword** 입니다.<br/><br/>기본값은 null입니다.|
|`public String getKeyStoreAuthentication()`|데이터 원본 개체에 대 한 Keyvault 인증 설정 값을 가져옵니다.|
|`public void setKeyStoreSecret(String keyStoreSecret)`|Java 키 저장소 암호를 설정 합니다. 키 저장소 및 키의 암호는 동일 해야 합니다. **JavaKeyStorePassword**를 사용 하 여 Keyvault 인증을 설정 해야 합니다.|
|`public void setKeyStoreLocation(String keyStoreLocation)`|Java 키 저장소의 파일 이름을 포함 하는 위치를 설정 합니다. **JavaKeyStorePassword**를 사용 하 여 Keyvault 인증을 설정 해야 합니다.|
|`public String getKeyStoreLocation()`|Java 키 저장소에 대 한 keyStoreLocation를 검색 합니다.|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 클래스**  
  
 Java 키 저장소에 대한 키 저장소 공급자의 구현입니다. 이 클래스를 사용하면 Java 키 저장소에 저장된 인증서를 열 마스터 키로 사용할 수 있습니다.  
  
 생성자  
  
|속성|설명|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionJavaKeyStoreProvider (String keyStoreLocation, char[] keyStoreSecret)`|Java 키 저장소에 대 한 키 저장소 공급자입니다.|  
  
 메서드  
  
|속성|설명|  
|----------|-----------------|  
|`public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)`|열 암호화 키의 지정된 암호화 값을 암호 해독합니다. 암호화 값은 지정된 키 경로가 있는 인증서와 지정된 알고리즘을 사용하여 암호화해야 합니다.<br /><br /> **키 경로 형식은 다음 중 하나여야 합니다.**<br /><br /> 지문:<certificate_thumbprint><br /><br /> 별칭:<certificate_alias><br /><br /> (SQLServerColumnEncryptionKeyStoreProvider를 재정의합니다. decryptColumnEncryptionKey(String, String, Byte[]).)|  
|`public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)`|지정된 키 경로가 있는 인증서와 지정된 알고리즘을 사용하여 열 암호화 키를 암호화합니다.<br /><br /> **키 경로 형식은 다음 중 하나여야 합니다.**<br /><br /> 지문:<certificate_thumbprint><br /><br /> 별칭:<certificate_alias><br /><br /> (SQLServerColumnEncryptionKeyStoreProvider를 재정의합니다. encryptColumnEncryptionKey(String, String, Byte[]).)|  
|`public void setName (String name)`|이 키 저장소 공급자의 이름을 설정 합니다.|
|`public String getName ()`|이 키 저장소 공급자의 이름을 가져옵니다.|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 클래스**  
  
 Azure Key Vault 저장소에 대한 키 저장소 공급자의 구현입니다. 이 클래스는 Azure Key Vault에 저장 된 키를 열 마스터 키로 사용할 수 있도록 합니다.  
  
 생성자  
  
|속성|설명|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionAzureKeyVaultProvider (String clientId, String clientKey)`|Azure Key Vault에 대 한 키 저장소 공급자입니다.  Azure Key Vault를 인증 하기 위해 토큰을 요청 하는 클라이언트의 키와 식별자를 제공 해야 합니다.|  
  
 메서드  
  
|속성|설명|  
|----------|-----------------|  
| `public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)` | CEK (암호화 된 열 암호화 키)를 Decryptes 합니다. 이 암호 해독은 마스터 키 경로에 지정 된 비대칭 키를 사용 하는 RSA 암호화 알고리즘을 사용 하 여 수행 됩니다.<br />(SQLServerColumnEncryptionKeyStoreProvider를 재정의합니다. decryptColumnEncryptionKey(String, String, Byte[]).) |  
| `public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)` | 지정 된 알고리즘에 지정 된 열 마스터 키를 제공 하 여 열 암호화 키를 암호화 합니다.<br />(SQLServerColumnEncryptionKeyStoreProvider를 재정의합니다. encryptColumnEncryptionKey(String, String, Byte[]).) |  
|`public void setName (String name)`|이 키 저장소 공급자의 이름을 설정 합니다.|
|`public String getName ()`|이 키 저장소 공급자의 이름을 가져옵니다.|  
  
  
 **SQLServerKeyVaultAuthenticationCallback Interface**  
  
 이 인터페이스에는 사용자가 구현 하는 Azure Key Vault 인증에 대 한 메서드가 포함 되어 있습니다.  
  
 메서드  
  
|속성|설명|  
|----------|-----------------|  
|`public String getAccessToken(String authority, String resource, String scope);`|메서드를 재정의 해야 합니다. 메서드는 Azure Key Vault에 대 한 액세스 토큰을 가져오는 데 사용 됩니다.|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 클래스**  
  
 사용자 지정 키 저장소 공급자를 구현하려면 이 클래스를 확장합니다.  
  
|속성|설명|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|모든 키 저장소 공급자에 대한 기본 클래스입니다. 사용자 지정 공급자는 이 클래스에서 파생되어 해당 멤버 함수를 재정의한 다음, SQLServerConnection을 사용하여 등록해야 합니다. registerColumnEncryptionKeyStoreProviders().|  
  
 메서드  
  
|속성|설명|  
|----------|-----------------|  
|`public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)`|열 암호화 키의 지정된 암호화 값을 암호 해독하는 기본 클래스 메서드입니다. 암호화된 값은 지정된 키 경로와 지정된 알고리즘이 있는 열 마스터 키를 사용하여 암호화해야 합니다.|  
|`public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)`|지정된 키 경로가 있는 열 마스터 키와 지정된 알고리즘을 사용하여 열 암호화 키를 암호화하기 위한 기본 클래스 메서드입니다.|
|`public abstract void setName(String name)`|이 키 저장소 공급자의 이름을 설정 합니다.|
|`public abstract String getName()`|이 키 저장소 공급자의 이름을 가져옵니다.|  
  
 **SQLServerPreparedStatement** 클래스의 새 메서드 또는 오버 로드 된 메서드  
  
|속성|설명|  
|----------|-----------------|  
|`public void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale)`<br /><br /> `public void setTime(int parameterIndex, java.sql.Time x, int scale)`<br /><br /> `public void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale)` <br />`public void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale)`|이러한 메서드는 전체 자릿수 및 소수 자릿수 정보를 필요로 하는 특정 데이터 형식에 대 한 Always Encrypted를 지원 하기 위해 전체 자릿수 또는 소수 자릿수 인수를 사용 하 여 오버 로드 됩니다.|  
|`public void setMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setSmallMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setUniqueIdentifier(int parameterIndex, String guid)`<br /><br /> `public void setDateTime(int parameterIndex, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(int parameterIndex, java.sql.Timestamp x)`|이러한 메서드는 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime 데이터 형식에 대 한 Always Encrypted를 지원 하기 위해 추가 되었습니다. <br/><br/>기존 `setTimestamp()` 메서드는 암호화 된 datetime2 열에 매개 변수 값을 보내는 데 사용 됩니다. 암호화 된 datetime 및 smalldatetime 열에는 `setDateTime()` `setSmallDateTime()` 각각 새 메서드와를 사용 합니다.|  
|`public final void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setSmallMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setBoolean(int parameterIndex, boolean x, boolean forceEncrypt)`<br /><br /> `public final void setByte(int parameterIndex, byte x, boolean forceEncrypt)`<br /><br /> `public final void setBytes(int parameterIndex, byte x[], boolean forceEncrypt)`<br /><br /> `public final void setUniqueIdentifier(int parameterIndex, String guid, boolean forceEncrypt)`<br /><br /> `public final void setDouble(int parameterIndex, double x, boolean forceEncrypt)`<br /><br /> `public final void setFloat(int parameterIndex, float x, boolean forceEncrypt)`<br /><br /> `public final void setInt(int parameterIndex, int value, boolean forceEncrypt)`<br /><br /> `public final void setLong(int parameterIndex, long x, boolean forceEncrypt)`<br /><br /> `public final setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale, boolean forceEncrypt)`<br /><br /> `public final void setShort(int parameterIndex, short x, boolean forceEncrypt)`<br /><br /> `public final void setString(int parameterIndex, String str, boolean forceEncrypt)`<br /><br /> `public final void setNString(int parameterIndex, String value, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setSmallDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setDate(int parameterIndex, java.sql.Date x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, java.util.Calendar cal, boolean forceEncrypt)`|지정된 매개 변수를 지정된 java 값으로 설정합니다.<br /><br /> 부울 forceEncrypt를 true로 설정 하면 지정 열이 암호화 되 고 연결 또는 문에서 Always Encrypted 사용 하도록 설정 된 경우에만 쿼리 매개 변수가 설정 됩니다.<br /><br /> 부울 forceEncrypt가 false로 설정 된 경우 드라이버는 매개 변수를 강제로 암호화 하지 않습니다.|  
  
 **SQLServerCallableStatement** 클래스의 새 메서드 또는 오버 로드 된 메서드  
  
|속성|설명|  
|----------|-----------------|  
|`public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)`<br />`public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale)`<br/><br/>`public final void setObject(String sCol, Object x, int targetSqlType, Integer precision, int scale)`|이러한 메서드는 전체 자릿수 및 소수 자릿수 정보를 필요로 하는 특정 데이터 형식에 대 한 Always Encrypted를 지원 하기 위해 전체 자릿수 또는 소수 자릿수 인수를 사용 하 여 오버 로드 됩니다.|  
|`public void setDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid)`<br /><br /> `public void setMoney(String parameterName, BigDecimal bd)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd)`<br/><br/>`public Timestamp getDateTime(int index)`<br/><br/>`public Timestamp getDateTime(String sCol)`<br/><br/>`public Timestamp getDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(int index)`<br/><br/>`public Timestamp getSmallDateTime(String sCol)`<br/><br/>`public Timestamp getSmallDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(String name, Calendar cal)`<br/><br/>`public BigDecimal getMoney(int index)`<br/><br/>`public BigDecimal getMoney(String sCol)`<br/><br/>`public BigDecimal getSmallMoney(int index)`<br/><br/>`public BigDecimal getSmallMoney(String sCol)`|이러한 메서드는 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime 데이터 형식에 대 한 Always Encrypted를 지원 하기 위해 추가 되었습니다. <br/><br/>기존 `setTimestamp()` 메서드는 암호화 된 datetime2 열에 매개 변수 값을 보내는 데 사용 됩니다. 암호화 된 datetime 및 smalldatetime 열에는 `setDateTime()` `setSmallDateTime()` 각각 새 메서드와를 사용 합니다.|  
|`public void setObject(String parameterName, Object o, int n, int m, boolean forceEncrypt)`<br /><br /> `public void setObject(String parameterName, Object obj, SQLType jdbcType, int scale, boolean forceEncrypt)`<br /><br /> `public void setDate(String parameterName, java.sql.Date x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale, boolean forceEncrypt)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid, boolean forceEncrypt)`<br /><br /> `public void setBytes(String parameterName, byte[] b, boolean forceEncrypt)`<br /><br /> `public void setByte(String parameterName, byte b, boolean forceEncrypt)`<br /><br /> `public void setString(String parameterName, String s, boolean forceEncrypt)`<br /><br /> `public final void setNString(String parameterName, String value, boolean forceEncrypt)<br /><br /> public void setMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public void setDouble(String parameterName, double d, boolean forceEncrypt)`<br /><br /> `public void setFloat(String parameterName, float f, boolean forceEncrypt)`<br /><br /> `public void setInt(String parameterName, int i, boolean forceEncrypt)`<br /><br /> `public void setLong(String parameterName, long l, boolean forceEncrypt)`<br /><br /> `public void setShort(String parameterName, short s, boolean forceEncrypt)`<br /><br /> `public void setBoolean(String parameterNames, boolean b, boolean forceEncrypt)`<br/><br/>`public void setTimeStamp(String sCol, java.sql.Timestamp x, Calendar c, Boolean forceEncrypt)`|지정된 매개 변수를 지정된 java 값으로 설정합니다.<br /><br /> 부울 forceEncrypt를 true로 설정 하면 지정 열이 암호화 되 고 연결 또는 문에서 Always Encrypted 사용 하도록 설정 된 경우에만 쿼리 매개 변수가 설정 됩니다.<br /><br /> 부울 forceEncrypt가 false로 설정 된 경우 드라이버는 매개 변수를 강제로 암호화 하지 않습니다.|
 

 **SQLServerResultSet** 클래스의 새 메서드 또는 오버 로드 된 메서드  
  
|속성|설명|  
|----------|-----------------|  
|`public String getUniqueIdentifier(int columnIndex)`<br/><br/>`public String getUniqueIdentifier(String columnLabel)`<br/><br/>   `public java.sql.Timestamp getDateTime(int columnIndex)` <br/><br/> `public java.sql.Timestamp getDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getDateTime(int columnIndex, Calendar cal)`   <br/><br/>`public java.sql.Timestamp getDateTime(String colName, Calendar cal)`    <br/><br/>`public java.sql.Timestamp getSmallDateTime(int columnIndex)`    <br/><br/> `public java.sql.Timestamp getSmallDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(int columnIndex, Calendar cal)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(String colName, Calendar cal)`   <br/><br/>  `public BigDecimal getMoney(int columnIndex)`  <br/><br/> `public BigDecimal getMoney(String columnName)`   <br/><br/> `public BigDecimal getSmallMoney(int columnIndex)`   <br/><br/>  `public BigDecimal getSmallMoney(String columnName)`  <br/><br/>`public void updateMoney(String columnName, BigDecimal x)`    <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x)`  <br/><br/>     `public void updateDateTime(int index, java.sql.Timestamp x)` <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x)` |이러한 메서드는 money, smallmoney, uniqueidentifier, datetime 및 smalldatetime 데이터 형식에 대 한 Always Encrypted를 지원 하기 위해 추가 되었습니다. <br/><br/>기존 `updateTimestamp()` 메서드는 암호화 된 datetime2 열을 업데이트 하는 데 사용 됩니다. 암호화 된 datetime 및 smalldatetime 열에는 `updateDateTime()` `updateSmallDateTime()` 각각 새 메서드와를 사용 합니다.|
|`public void updateBoolean(int index, boolean x, boolean forceEncrypt)`  <br/><br/>  `public void updateByte(int index, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(int index, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(int index, int x, boolean forceEncrypt)`   <br/><br/>  `public void updateLong(int index, long x, boolean forceEncrypt)`  <br/><br/> `public void updateFloat(int index, float x, boolean forceEncrypt)`   <br/><br/> `public void updateDouble(int index, double x, boolean forceEncrypt)`   <br/><br/> `public void updateMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateSmallMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateBigDecimal(int index, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateString(int columnIndex, String stringValue, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(int columnIndex, String nString, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(String columnLabel, String nString, boolean forceEncrypt)`  <br/><br/> `public void updateBytes(int index, byte x[], boolean forceEncrypt)   <br/><br/>  public void updateDate(int index, java.sql.Date x, boolean forceEncrypt)`  <br/><br/> `public void updateTime(int index, java.sql.Time x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateTimestamp(int index, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/> `public void updateDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateUniqueIdentifier(int index, String x, boolean forceEncrypt)`    <br/><br/>  `public void updateObject(int index, Object x, int precision, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateObject(int index, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateBoolean(String columnName, boolean x, boolean forceEncrypt)`    <br/><br/>  `public void updateByte(String columnName, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(String columnName, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(String columnName, int x, boolean forceEncrypt)`   <br/><br/>   `public void updateLong(String columnName, long x, boolean forceEncrypt)` <br/><br/>  `public void updateFloat(String columnName, float x, boolean forceEncrypt)`  <br/><br/>  `public void updateDouble(String columnName, double x, boolean forceEncrypt)  <br/><br/> public void updateBigDecimal(String columnName, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateBigDecimal(String columnName, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateString(String columnName, String x, boolean forceEncrypt)`   <br/><br/>  `public void updateBytes(String columnName, byte x[], boolean forceEncrypt)`  <br/><br/> `public void updateDate(String columnName, java.sql.Date x, boolean forceEncrypt)`   <br/><br/>  `public void updateTime(String columnName, java.sql.Time x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateTimestamp(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateUniqueIdentifier(String columnName, String x, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object x, int precision, int scale, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`|지정 된 열을 지정 된 java 값으로 업데이트 합니다.<br/><br/>부울 forceEncrypt가 true로 설정 된 경우에는 열이 암호화 되 고 연결 또는 문에서 Always Encrypted 설정 된 경우에만 설정 됩니다.<br/><br/>부울 forceEncrypt가 false로 설정 된 경우 드라이버는 매개 변수를 강제로 암호화 하지 않습니다.|

  
**Microsoft .Sql types** 클래스의 새 형식

|속성|설명|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|API 메서드를 사용 하 여 `setObject()/updateObject()` **암호화 된** datetime, smalldatetime, money, smallmoney, uniqueidentifier 열에 매개 변수 값을 전송할 때 이러한 형식을 대상 SQL 형식으로 사용 합니다.|  
  
  
 **SQLServerStatementColumnEncryptionSetting 열거형**  
  
 암호화 된 열을 읽고 쓸 때 데이터를 보내고 받는 방법을 지정 합니다. 특정 쿼리에 따라 암호화 되지 않은 열을 사용 하는 경우 Always Encrypted 드라이버의 처리를 무시 하 여 성능 영향을 줄일 수 있습니다. 이러한 설정을 사용 하 여 암호화를 무시 하 고 일반 텍스트 데이터에 대 한 액세스를 얻을 수는 없습니다.  
  
 **구문**  
  
```java
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **멤버**  
  
|속성|설명|  
|----------|-----------------|  
|UseConnectionSetting|명령이 연결 문자열의 Always Encrypted 설정에 기본적으로 지정 되도록 지정 합니다.|  
|설정|쿼리에 Always Encrypted를 사용 하도록 설정 합니다.|  
|ResultSetOnly|명령의 결과만 드라이버의 Always Encrypted 루틴에서 처리 하도록 지정 합니다. 명령에 암호화가 필요한 매개 변수가 없는 경우이 값을 사용 합니다.|  
|사용 안 함|쿼리에 Always Encrypted를 사용 하지 않도록 설정 합니다.|  
  
 AE에 대 한 문 수준 설정은 SQLServerConnection 클래스 및 SQLServerConnectionPoolProxy 클래스에 추가 됩니다. 이러한 클래스의 다음 메서드는 새 설정으로 오버 로드 됩니다.  
  
|속성|설명|  
|----------|-----------------|  
|`public Statement createStatement(int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|지정 된 형식, 동시성, 유지 기능 및 열 암호화 설정을 사용 하 여 ResultSet 개체를 생성 하는 문 개체를 만듭니다.|  
|`public CallableStatement prepareCall(String sql, int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)`|지정 된 형식, 동시성 및 유지 기능를 사용 하 여 결과 집합 개체를 생성 하는 지정 된 열 암호화 설정을 사용 하 여 CallableStatement 개체를 만듭니다.|  
|`public PreparedStatement prepareStatement(String sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|자동 생성 키를 검색할 수 있는 기능이 있는 지정 된 열 암호화 설정을 사용 하 여 Java.sql.preparedstatement 개체를 만듭니다.|  
|`public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|지정 된 열 이름을 사용 하 여 결과 집합 개체를 생성 하는 지정 된 열 암호화 설정을 사용 하 여 Java.sql.preparedstatement 개체를 만듭니다.|  
|`public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting`|지정 된 열 인덱스를 사용 하 여 결과 집합 개체를 생성 하는 지정 된 열 암호화 설정을 사용 하 여 Java.sql.preparedstatement 개체를 만듭니다.|  
|`public PreparedStatement prepareStatement(String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|지정 된 형식, 동시성 및 유지 기능를 사용 하 여 결과 집합 개체를 생성 하는 지정 된 열 암호화 설정을 사용 하 여 Java.sql.preparedstatement 개체를 만듭니다.|  
  
> [!NOTE]  
>  쿼리에 대해 Always Encrypted를 사용 하지 않도록 설정 하 고 쿼리에 암호화 해야 하는 매개 변수 (암호화 된 열에 해당 하는 매개 변수)가 있는 경우 쿼리가 실패 합니다.  
>   
>  쿼리에 대해 Always Encrypted를 사용 하지 않도록 설정 하 고 쿼리가 암호화 된 열에서 결과를 반환 하는 경우 쿼리는 암호화 된 값을 반환 합니다. 암호화 된 값에는 varbinary 데이터 형식이 있습니다.  
  
 ## <a name="see-also"></a>관련 항목:  
 [Always Encrypted와 JDBC 드라이버 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

