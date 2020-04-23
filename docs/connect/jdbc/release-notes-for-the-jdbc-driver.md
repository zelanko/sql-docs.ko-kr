---
title: JDBC 드라이버에 대한 릴리스 정보
description: 이 문서에는 SQL Server용 Microsoft JDBC Driver의 릴리스가 나열되어 있습니다. 릴리스 버전별로 변경 내용을 밝히고 설명합니다.
ms.custom: ''
ms.date: 03/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbcff4ee14db85a3a973496ce8a5cb24772a35b9
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634290"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver-for-sql-server"></a>SQL Server용 Microsoft JDBC 드라이버에 대한 릴리스 정보

이 문서에는 _SQL Server용 Microsoft JDBC Driver_의 릴리스가 나열되어 있습니다. 릴리스 버전별로 변경 내용을 밝히고 설명합니다.

## <a name="82"></a><a id="82"></a> 8.2

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 8.2(zip) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122433)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 8.2(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122536)**  

버전 번호: 8.2.2 릴리스 날짜: 2020년 3월 24일

검색된 언어가 아닌 다른 언어로 드라이버를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
zip 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x40a)  
tar.gz 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x40a)  

### <a name="compliance"></a>규정 준수

| 규정 준수 변경 | 세부 정보 |
| :---------------- | :------ |
| JDBC Driver 8.2의 최신 업데이트를 다운로드합니다. | &bull; &nbsp; [GitHub, 8.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v8.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 사양 4.2를 완벽히 준수합니다. | 8\.2 패키지의 jar는 Java 버전 호환성에 따라 이름이 지정됩니다.<br/><br/>예를 들어 8.2 패키지의 mssql-jdbc-8.2.2.jre11.jar 파일은 Java 11과 함께 사용해야 합니다. |
| JDK(Java Development Kit) 버전 13.0, 11.0 및 1.8과 호환됩니다. | SQL Server용 Microsoft JDBC Driver 8.2는 이제 JDK 11.0 및 1.8 외에도 JDK(Java Development Kit) 버전 13.0과도 호환됩니다. |
| &nbsp; | &nbsp; |

### <a name="support-for-jdk-13"></a>JDK 13 지원

SQL Server용 Microsoft JDBC Driver 8.2는 이제 JDK 11.0 및 1.8 외에도 JDK(Java Development Kit) 버전 13.0과도 호환됩니다.

### <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted

| Always Encrypted 변경 | 세부 정보 |
| :--------- | :------ |
| SQL Server용 Microsoft JDBC Driver 8.2는 이제 보안 Enclave를 사용한 Always Encrypted를 지원합니다. 자세한 내용은 여기에서 찾을 수 있습니다. 보안 enclave를 사용한 Always Encrypted. |
| 추가 정보 및 샘플 코드. | [보안 Enclave를 사용한 Always Encrypted](always-encrypted-with-secure-enclaves.md)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="performance-improvement-when-retrieving-temporal-datatypes-from-sql-server-sup1sup"></a>SQL Server에서 Temporal 데이터 형식을 검색하는 경우의 성능 향상<sup>1</sup>

| Temporal 데이터 형식 변경 | 세부 정보 |
| :---------- | :------ |
| SQL Server용 Microsoft JDBC Driver 8.2는 SQL Server에서 Temporal 데이터 형식을 검색하는 경우의 성능이 향상되었습니다. | 이 변경으로 인해 가능한 경우 항상 java.util.Calendar를 사용하지 않아 불필요한 temportal 데이터 형식을 변환할 필요가 없습니다. |
| 다음은 이 성능 향상의 영향을 받은 temporal 데이터 형식 목록이며, SQL Server 데이터 형식 뒤에 각 Java 매핑이 오는 형식입니다. | date (java.sql.Date), datetime (java.sql.Timestamp), datetime2 (java.sql.Timestamp), smalldatetime (java.sql.Timestamp) 및 time (java.sql.Time). |
| &nbsp; | &nbsp; |

<sup>1</sup> java.util.Calendar 및 java.time.LocalDateTime API에서 표준 시간대가 처리되는 방법의 차이로 인해 사용자가 제공한 java.util.Calendar 개체가 연결된 temporal 데이터 형식 또는 microsoft.sql.DateTimeOffset 데이터 형식은 이 향상된 기능을 이용하지 않습니다.

### <a name="deployment-of-mssql-jdbc_auth-version-archdll-previously-sqljdbc_authdll-to-maven-repository"></a>Maven 리포지토리에 mssql-jdbc_auth-\<버전>-\<arch>.dll(이전 sqljdbc_auth.dll) 배포

| sqljdbc_auth.dll 변경 | 세부 정보 |
| :------------------- | :------ |
| SQL Server용 Microsoft JDBC Driver 8.2부터, 드라이버는 sqljdbc_auth.dll이 아니라 mssql-jdbc_auth-\<버전>-\<arch>.dll을 통해 Azure Active Directory 인증 기능을 사용합니다. | &nbsp; |
| 또한 더 쉽게 액세스할 수 있도록 DLL이 Maven 리포지토리에 업로드되었습니다. | [이 페이지](https://search.maven.org/artifact/com.microsoft.sqlserver/mssql-jdbc_auth)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

| 알려진 문제 | 세부 정보 |
| :----------- | :------ |
| Java 8에서 보안 Enclave를 사용한 Always Encrypted를 사용할 경우. | 사용자는 종속성으로 BouncyCastle 공급자를 포함하거나 RSASSA-PSS 서명 알고리즘을 지원하는 보안 공급자를 매핑/로드해야 합니다. |
| &nbsp; | &nbsp; |

## <a name="previous-releases"></a>이전 릴리스

## <a name="a-id74-741"></a><a id="74"> 7.4.1

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 7.4.1(자동 압축 풀기 exe) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122712)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 7.4.1(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122613)**  

버전 번호: 7.4.1  
릴리스 날짜: 2019년 8월 2일

검색된 언어가 아닌 다른 언어로 드라이버를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
자동 압축 풀기 exe 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x40a)  
tar.gz 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x40a)  

### <a name="compliance"></a>규정 준수

| 규정 준수 변경 | 세부 정보 |
| :---------------- | :------ |
| JDBC Driver 7.4의 최신 업데이트를 다운로드합니다. | &bull; &nbsp; [GitHub, 7.4.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.4.1)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 사양 4.2를 완벽히 준수합니다. | 7\.4 패키지의 jar는 Java 버전 호환성에 따라 이름이 지정됩니다.<br/><br/>예를 들어 7.4 패키지의 mssql-jdbc-7.4.1.jre11.jar 파일은 Java 11과 함께 사용해야 합니다. |
| JDK(Java Development Kit) 버전 12.0, 11.0 및 1.8과 호환됩니다. | SQL Server용 Microsoft JDBC Driver 7.4는 이제 JDK 11.0 및 1.8 외에도 JDK(Java Development Kit) 버전 12.0과도 호환됩니다. |
| &nbsp; | &nbsp; |

### <a name="support-for-jdk-12"></a>JDK 12 지원

SQL Server용 Microsoft JDBC Driver 7.4는 이제 JDK 11.0 및 1.8 외에도 JDK(Java Development Kit) 버전 12.0과도 호환됩니다.

### <a name="introduces-ntlm-authentication"></a>NTLM 인증 소개

| NTLM 변경 | 세부 정보 |
| :--------- | :------ |
| NTLM 인증 모드를 지원합니다. | 이 인증 모드를 사용하면 Windows 및 다른 운영 체제의 클라이언트가 모두 Windows 도메인 사용자를 사용하여 SQL Server에 대해 자신을 인증할 수 있습니다. |
| 이 인증 모드를 사용하기 위한 자세한 내용 및 애플리케이션 예제 | [NTLM 인증을 사용하여 연결](using-ntlm-authentication-to-connect-to-sql-server.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="introduces-querying-parametermetadata-via-_usefmtonly_"></a>_useFmtOnly_를 통해 ParameterMetaData 쿼리를 소개

| useFmtOnly 변경 | 세부 정보 |
| :---------- | :------ |
| **useFmtOnly** 연결 속성이 추가되었습니다. | 이 기능을 사용하면 `SET FMTONLY ON` 레거시 API를 통해 ParameterMetaData를 선택적으로 쿼리할 수 있습니다. 이 기능은 `sp_describe_undeclared_parameters`가 예상대로 작동하지 않는 시나리오에 유용합니다. |
| 세부 사항 및 제한 사항 | [useFmtOnly 사용](using-usefmtonly.md) 참조 |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-121"></a>업데이트된 _Java용 Microsoft Azure Key Vault SDK_ 버전: 1.2.1

| Key Vault SDK 변경 | 세부 정보 |
| :------------------- | :------ |
| _Java용 Microsoft Azure Key Vault SDK_의 Maven 종속성을 버전 1.2.1로 업데이트했습니다. | &nbsp; |
| _Key Vault WebKey용 Microsoft Azure SDK_를 Maven 종속성에서 제거합니다. | &nbsp; |
| 추가 정보 | [SQL Server용 Microsoft JDBC Driver의 기능 종속성](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

| 알려진 문제 | 세부 정보 |
| :----------- | :------ |
| NTLM 인증을 사용하는 경우 | 확장 보호 및 암호화된 연결을 동시에 활성화하는 기능은 현재 지원되지 않습니다. |
| useFmtOnly를 사용하는 경우 | 이 기능에는 SQL 구문 분석 논리의 결함으로 인해 발생하는 몇 가지 문제가 있습니다. 자세한 내용 및 해결 방법에 관한 제안은 [useFmtOnly 사용](using-usefmtonly.md)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="a-id72-722"></a><a id="72"> 7.2.2

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 7.2.2(자동 압축 풀기 exe) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122435)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 7.2.2(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122434)**  

버전 번호: 7.2.2  
릴리스 날짜: 2019년 4월 16일

검색된 언어가 아닌 다른 언어로 드라이버를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
자동 압축 풀기 exe 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x40a)  
tar.gz 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x40a)  

### <a name="compliance"></a>규정 준수

| 규정 준수 변경 | 세부 정보 |
| :---------------- | :------ |
| JDBC Driver 7.2의 최신 업데이트를 다운로드합니다. | &bull; &nbsp; [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 사양 4.2를 완벽히 준수합니다. | 7\.2 패키지의 jar는 Java 버전 호환성에 따라 이름이 지정됩니다.<br/><br/>예를 들어 7.2 패키지의 mssql-jdbc-7.2.2.jre11.jar 파일은 Java 11과 함께 사용해야 합니다. |
| JDK 1.8 외에도 JDK(Java Development Kit) 버전 11.0을 지원합니다. | SQL Server용 Microsoft JDBC Driver 7.2는 이제 JDK 1.8 외에도 JDK(Java Development Kit) 버전 11.0과도 호환됩니다. |
| &nbsp; | &nbsp; |

> [!NOTE]
> 2019년 1월 31일에 릴리스된 JDBC 7.2 RTW(Release To Web) 드라이버에서 SQL 문 구문 분석 문제를 찾았습니다. 변경 내용은 롤백되었고 새 jar(버전 7.2.1)가 2019년 2월 11일에 릴리스되었습니다.
>
> ActivityID가 제대로 정리되지 않는 문제를 수정하기 위해 드라이버가 또 한번 업데이트되었습니다. 새 jar(버전 7.2.2)는 2019년 4월 16일에 릴리스되었습니다.
>
> 7\.2.2 릴리스 jar를 사용하도록 프로젝트를 업데이트하는 것이 좋습니다. 자세한 내용은 [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1) 및 [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)의 릴리스 정보를 참조하세요.

### <a name="active-directory-_managed-service-identity_-msi-authentication"></a>Active Directory MSI(관리 서비스 ID)  인증

| MSI 변경 | 세부 정보 |
| :--------- | :------ |
| Active Directory Service MSI(관리 서비스 ID) 인증 모드를 지원합니다. | 이 인증 모드는 ‘ID’ 기능 지원을 사용하도록 설정한 Azure 리소스에 사용할 수 있습니다.<br/><br/>드라이버에서 **accessToken**을 가져와 보안 연결을 설정하기 위해 MSI(관리 시스템 ID)의 두 가지 유형이 모두 지원됩니다. |
| 이 인증 모드를 사용하기 위한 자세한 내용 및 애플리케이션 예제 | [Azure Active Directory 인증을 사용하여 연결](connecting-using-azure-active-directory-authentication.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="introduces-_open-service-gateway-initiative_-osgi-support"></a>_OSGi(Open Service Gateway Initiative)_ 지원 소개

| OSGi 변경 | 세부 정보 |
| :---------- | :------ |
| **DataSourceFactory** 구현이 추가되었습니다. | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| **Activator** 구현이 추가되었습니다. | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-_sqlservererror_-apis"></a>_SQLServerError_ API 소개

| 오류 API 변경 | 세부 정보 |
| :--------------- | :------ |
| SQLServerError API가 도입되었습니다. | 서버에서 생성된 오류에 대한 추가 정보를 검색하는 Getter API입니다.<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| 추가 정보 | [오류 처리](handling-errors.md)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-active-directory-authentication-library-adal4j-for-java_-version-163"></a>업데이트된 _ADAL4J(Java용 Microsoft Azure Active Directory 인증 라이브러리)_ 버전: 1.6.3

| ADAL4J 변경 | 세부 정보 |
| :------------ | :------ |
| ADAL4J에 대한 Maven 종속성을 버전 1.6.3으로 업데이트했습니다. | &nbsp; |
| ‘AutoRest용 Java 클라이언트 런타임’을  Maven 종속성 버전 1.6.5로 도입합니다. | &nbsp; |
| 추가 정보 | [SQL Server용 Microsoft JDBC Driver의 기능 종속성](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-120"></a>Java용 Microsoft Azure Key Vault SDK  버전 1.2.0 업데이트

| Key Vault SDK 변경 | 세부 정보 |
| :------------------- | :------ |
| ‘Java용 Microsoft Azure Key Vault SDK’에 대한  Maven 종속성을 버전 1.2.0으로 업데이트했습니다. | &nbsp; |
| _Key Vault WebKey용 Microsoft Azure SDK_를 Maven 종속성(버전 1.2.0.)을 소개합니다. | &nbsp; |
| 추가 정보 | [SQL Server용 Microsoft JDBC Driver의 기능 종속성](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

| 알려진 문제 | 세부 정보 |
| :----------- | :------ |
| 일부 경우의 매개 변수가 있는 쿼리 | 이 문제를 해결하기 위해 7.2.0 버전의 업데이트 v7.2.1이 2019년 2월에 릴리스되었습니다. |
| ActivityId 정리 | 이 문제를 해결하기 위해 7.2.1 버전의 업데이트 v7.2.2가 2019년 4월에 릴리스되었습니다. |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 7.0(자동 압축 풀기 exe) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122713)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 7.0(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122614)**  

버전 번호: 7.0.0  
릴리스 날짜: 2018년 7월 31일

검색된 언어가 아닌 다른 언어로 드라이버를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
자동 압축 풀기 exe 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x40a)  
tar.gz 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x40a)  

SQL Server용 Microsoft JDBC Driver 7.0은 JDBC API 사양 4.2를 완벽하게 준수합니다. 7\.0 패키지의 jar는 Java 버전 호환성에 따라 이름이 지정됩니다. 예를 들어 7.0 패키지의 mssql-jdbc-7.0.0.jre10.jar 파일은 Java 10과 함께 사용해야 합니다.

### <a name="support-for-jdk-10"></a>JDK 10 지원

SQL Server용 Microsoft JDBC Driver 7.0은는 이제 JDK 1.8 외에도 JDK(Java Development Kit) 버전 10.0과도 호환됩니다. 이 업데이트는 매니페스트 파일을 통해 드라이버의 `Automatic-Module-Name`도 `com.microsoft.sqlserver.jdbc`로 노출합니다.

### <a name="support-for-spatial-datatypes"></a>공간 데이터 형식 지원

SQL Server용 Microsoft JDBC Driver 7.0은 이제 SQL Server 공간 데이터 형식 Geography 및 Geometry를 지원합니다. 공간 데이터 형식 API 및 사용 방법에 대한 자세한 내용은 [Using spatial datatypes](use-spatial-datatypes.md)(공간 데이터 형식 사용)를 참조하세요.

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>JDBC 4.3에서 도입된 java.sql.Connection API beginRequest() 및 endRequest()에 대한 구현

SQL Server용 Microsoft JDBC Driver 7.0은 이제 `java.sql.Connection` 클래스에서 `beginRequest()` 및 `endRequest()` API를 구현합니다. 이러한 API는 JDBC 4.3 사양 및 JDK 9에서 도입되었습니다. 드라이버의 이러한 API 구현에 대한 자세한 내용은 Api의 드라이버의 구현에 대한 자세한 내용은 참조하세요. [JDBC 4.3 compliance for the JDBC Driver](jdbc-4-3-compliance-for-the-jdbc-driver.md)(JDBC Driver의 JDBC 4.3 준수)를 참조하세요.

### <a name="support-for-sql-data-discovery-and-classification"></a>SQL 데이터 검색 및 분류 지원

SQL Server용 Microsoft JDBC Driver 7.0은 SQL 데이터 검색 및 분류 기능을 해당 기능을 지원하는 모든 대상 데이터베이스에서 지원합니다. 이제 드라이버는 `SQLServerResultSet.getSensitivityClassification()` API를 노출하여 가져온 `ResultSet`에서 이 정보를 추출합니다.

JDBC 드라이버에서 이 기능을 사용하는 방법에 대한 자세한 내용은 [SQL 데이터 검색 및 분류](data-discovery-classification-sample.md)를 참조하세요.

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>추가된 연결 속성: useBulkCopyForBatchInsert

SQL Server용 Microsoft JDBC Driver 7.0은 새 연결 속성 `useBulkCopyForBatchInsert`를 도입합니다. 이 속성은 Azure SQL Data Warehouse에서만 지원됩니다.

이 속성은 기본적으로 사용되지 않습니다. Azure SQL Data Warehouse로 많은 양의 데이터를 푸시하는 경우 이 기능을 사용하도록 설정하여 사용자 애플리케이션의 성능을 향상할 수 있습니다. 이 속성을 사용하도록 설정하면 일괄 삽입 작업의 동작이 바뀌어 사용자가 지정한 데이터를 사용한 대량 복사 작업으로 전환됩니다. 이 속성 및 해당 제한 사항에 대한 자세한 내용은 [Using Bulk Copy API for batch insert operation](use-bulk-copy-api-batch-insert-operation.md)(일괄 삽입 작업에 대량 복사 API 사용)을 참조하세요.

### <a name="added-connection-property-cancelquerytimeout"></a>추가된 연결 속성: cancelQueryTimeout

SQL Server용 Microsoft JDBC Driver 7.0은 새 연결 속성 `cancelQueryTimeout`을 도입합니다. 이 속성은 `java.sql.Connection` 및 `java.sql.Statement` 개체의 `queryTimeout`을 취소합니다.

### <a name="added-azure-key-vault-provider-constructors"></a>Azure Key Vault 공급자 생성자 추가

SQL Server용 Microsoft JDBC Driver 7.0은 이전에 제거된 `SQLServerColumnEncryptionAzureKeyVaultProvider`의 생성자를 다시 도입합니다. 이 생성자를 사용하면 `SQLServerKeyVaultAuthenticationCallback`에서 구현된 사용자 지정 메서드를 통해 액세스 토큰을 가져올 수 있었습니다.

새 생성자의 정의는 다음과 같습니다.

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>업데이트된 "ADAL4J(Java용 Microsoft Azure Active Directory 인증 라이브러리)" 버전: 1.6.0

SQL Server용 Microsoft JDBC Driver 7.0에서는 “ADAL4J(Java용 Microsoft Azure Active Directory 인증 라이브러리)"에 대한 Maven 종속성을 버전 1.6.0으로 업데이트했습니다. 종속성에 대한 자세한 내용은 [Feature dependencies of the Microsoft JDBC Driver for SQL Server](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)(SQL Server용 Microsoft JDBC Driver의 기능 종속성)를 참조하세요.

## <a name="64"></a>6.4

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 6.4(자동 압축 풀기 exe) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122436)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 6.4(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122537)**  

버전 번호: 6.4.0  
릴리스 날짜: 2018년 2월 27일

검색된 언어가 아닌 다른 언어로 드라이버를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
자동 압축 풀기 exe 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x40a)  
tar.gz 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x40a)  

SQL Server용 Microsoft JDBC Driver 6.4는 JDBC API 사양 4.1 및 4.2를 완벽하게 준수합니다. 6\.4 패키지의 jar는 Java 버전 호환성에 따라 이름이 지정됩니다. 예를 들어 6.4 패키지의 mssql-jdbc-6.4.0.jre8.jar 파일은 Java 8과 함께 사용해야 합니다.

### <a name="support-for-jdk-9"></a>JDK 9 지원

이 드라이버에서는 JDK 8.0 및 7.0 외에도 JDK 버전 9.0을 지원합니다.

### <a name="jdbc-43-compliance"></a>JDBC 4.3 준수

드라이버는 4.1 및 4.2 외에도 Java Database Connectivity API 4.3 사양을 지원합니다. JDBC 4.3 API 메서드가 추가되었지만 아직 구현되지 않았습니다. 자세한 내용은 [JDBC Driver의 JDBC 4.3 준수](jdbc-4-3-compliance-for-the-jdbc-driver.md)를 참조하세요.

### <a name="added-connection-property-sslprotocol"></a>추가된 연결 속성: sslProtocol

새 연결 속성을 사용하면 TLS 프로토콜 키워드를 지정할 수 있습니다. 가능한 값은 다음과 같습니다. "TLS", "TLSv1", "TLSv1.1" 및 "TLSv1.2". 자세한 내용은 [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)을 참조하세요.

### <a name="deprecated-connection-property-fipsprovider"></a>사용되지 않는 연결 속성: fipsProvider

연결 속성 `fipsProvider`가 허용되는 연결 속성 목록에서 제거되었습니다. 자세한 내용은 [GitHub pull request](https://github.com/Microsoft/mssql-jdbc/pull/460)(GitHub 끌어오기 요청)를 참조하세요.

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>사용자 지정 TrustManager를 지정하기 위한 연결 속성 추가

이제는 드라이버에서 추가된 `trustManagerClass` 및 `trustManagerConstructorArg` 연결 속성을 사용하여 사용자 지정 TrustManager를 지정할 수 있습니다. JVM(Java Virtual Machine) 환경의 전역 설정을 수정하지 않고 연결별로 신뢰할 수 있는 인증서 집합을 동적으로 지정할 수 있습니다.

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>테이블 반환 매개 변수에서 datetime/smallDatetime에 대한 지원 추가

이제 드라이버에서 TVP(테이블 반환 매개 변수)를 사용할 때 데이터 형식 `datetime` 및 `smallDatetime`을 지원합니다.

### <a name="added-support-for-the-sql_variant-datatype"></a>sql_variant 데이터 형식에 대한 지원 추가

이제 JDBC Driver에서는 `sql_variant` 데이터 형식을 SQL Server와 함께 사용할 수 있습니다. `sql_variant` 데이터 형식도 TVP 및 대량 복사와 같은 기능에서 지원됩니다. 단, 여기에는 다음과 같은 제한 사항이 있습니다.

* **날짜 값**:

  TVP를 사용하여 `sql_variant` 열에 저장된 `datetime`, `smalldatetime` 또는 `date`를 포함하는 테이블을 채울 때 결과 세트에 대해 `getDateTime()`, `getSmallDateTime()` 또는 `getDate()` 메서드를 호출하면 제대로 작동하지 않고 다음 예외가 throw됩니다.

  `java java.lang.String cannot be cast to java.sql.Timestamp`

  해결 방법으로 `getString()` 또는 `getObject()` 메서드를 사용합니다.

* **null 값에 대한 sql_variant로 TVP 사용**:
  
  TVP를 사용하여 테이블을 채우고 NULL 값을 `sql_variant` 열 형식에 보낼 경우 예외가 발생합니다. TVP에서 열 형식 `sql_variant`를 사용한 NULL 값 삽입은 현재 지원되지 않습니다.

### <a name="implemented-prepared-statement-metadata-caching"></a>준비된 문 메타데이터 캐싱이 구현됨

JDBC Driver에서 성능 향상을 위해 준비된 문 메타데이터 캐싱을 구현했습니다. 드라이버는 이제 `disableStatementPooling` 및 `statementPoolingCacheSize` 연결 속성을 사용하여 드라이버에서 준비된 문 메타데이터 캐싱을 지원합니다. 이 기능은 기본적으로 해제되어 있습니다. 자세한 내용은 [Prepared statement metadata caching for the JDBC Driver](prepared-statement-metadata-caching-for-the-jdbc-driver.md)(JDBC Driver에 대한 준비된 문 메타데이터 캐싱)를 참조하세요.

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmacos"></a>Linux/macOS에서 Azure AD 통합 인증에 대한 지원 추가

또한 JDBC Driver는 이제 지원되는 모든 운영 체제(Windows, Linux, macOS)에서 Kerberos를 사용하여 Azure AD(Azure Active Directory) 통합 인증을 지원합니다. 또는 Windows 운영 체제에서 사용자는 mssql-jdbc_auth-\<버전>-\<arch>.dll을 사용하여 인증할 수 있습니다.

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>업데이트된 "ADAL4J(Java용 Microsoft Azure Active Directory 인증 라이브러리)" 버전: 1.4.0

JDBC Driver에서 “ADAL4J(Java용 Microsoft Azure Active Directory 인증 라이브러리)"에 대한 Maven 종속성을 버전 1.4.0으로 업데이트했습니다. 종속성에 대한 자세한 내용은 [Feature dependencies of the Microsoft JDBC Driver for SQL Server](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)(SQL Server용 Microsoft JDBC Driver의 기능 종속성)를 참조하세요.

## <a name="62"></a>6.2

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 6.2(자동 압축 풀기 exe) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122616)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 6.2(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122615)**  

버전 번호: 6.2.2  
릴리스 날짜: 2017년 9월 29일

검색된 언어가 아닌 다른 언어로 드라이버를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
자동 압축 풀기 exe 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x40a)  
tar.gz 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x40a)  

SQL Server용 Microsoft JDBC Driver 6.2는 JDBC API 사양 4.1 및 4.2를 완벽하게 준수합니다. 6\.2 패키지의 jar는 Java 버전 호환성에 따라 이름이 지정됩니다. 예를 들어 6.2 패키지의 mssql-jdbc-6.2.2.jre8.jar 파일은 Java 8과 함께 사용해야 합니다.

> [!NOTE]  
> 2017년 6월 29일에 릴리스된 JDBC 6.2 RTW에서 메타데이터 캐싱 개선 관련 문제가 발견되었습니다. 개선 내용은 롤백되었고 새 jar(버전 6.2.1)가 2017년 7월 17일에 릴리스되었습니다.
>
> 또 한번의 개선에서 Azure Key Vault 종속 라이브러리 버전을 1.0.0으로 업그레이드했고 새 jar(버전 6.2.2)가 2017년 10월 19일에 릴리스되었습니다.
>
> 위 링크, [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) 또는 [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver)에서 JDBC Driver 6.2의 최신 업데이트를 다운로드하세요. 6\.2.2 릴리스 jar를 사용하도록 프로젝트를 업데이트하세요. 자세한 내용은 [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) 및 [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2)의 릴리스 정보를 참조하세요.

### <a name="azure-ad-support-for-linux"></a>Linux에 대한 Azure AD 지원

사용자 이름/암호 및 액세스 토큰 방법을 통해 Azure AD 인증을 사용하여 Azure SQL Database에 Linux 애플리케이션을 연결합니다.

### <a name="fips-enabled-jvms"></a>FIPS 사용 JVM

이제 JDBC Driver는 FIPS(Federal Information Processing Standard) 140 준수 모드에서 실행되는 JVM에서 사용하여 준수에 대한 연방 표준을 충족할 수 있습니다.

### <a name="kerberos-authentication-improvements"></a>Kerberos 인증 향상

JDBC Driver에서 이제 다음을 지원합니다.

* Kerberos 구성을 수정할 수 없거나 새 토큰 또는 keytab을 검색할 수 없는 애플리케이션에 대한 보안 주체/암호 방식. 이 방법을 사용하여 Kerberos 인증만 허용하는 SQL Server 인스턴스를 인증할 수 있습니다.
* 서버 SPN을 명시적으로 설정하지 않고 Kerberos 통합 인증을 사용하는 영역 간 인증. 이제 드라이버에서는 영역이 제공되지 않은 경우에도 영역을 자동으로 계산합니다.
* 가장된 사용자 자격 증명을 데이터 원본을 통해 GSS 자격 증명 개체로 사용할 수 있도록 하는 Kerberos 제한 위임. 그런 다음 이 가장된 자격 증명을 사용하여 Kerberos 연결을 설정합니다.

### <a name="added-timeouts"></a>추가된 시간 제한

JDBC Driver에서는 이제 다음과 같은 구성 가능한 시간 제한을 지원합니다. 애플리케이션의 필요에 따라 시간 제한을 변경할 수 있습니다.

* 쿼리를 실행할 때 시간 초과가 발생하기 전까지 대기할 시간(초)를 제어하는 쿼리 시간 제한
* 소켓 일기 또는 허용에서 시간 초과가 발생하기 전까지 대기할 시간(밀리초)을 지정하는 소켓 시간 제한

## <a name="61"></a>6.1

버전 번호: 6.1.0  
릴리스 날짜: 2016년 11월 17일  

SQL Server용 Microsoft JDBC Driver 6.1은 JDBC API 사양 4.1 및 4.2를 완벽하게 준수합니다. 이 버전은 JDBC Driver의 최초 오픈 소스 릴리스입니다. 소스 코드는 [GitHub v6.1.0 태그](https://github.com/microsoft/mssql-jdbc/releases/tag/v6.1.0)에서 찾을 수 있습니다. 소스 코드는 Java 버전 호환성에 해당하는 mssql-jdbc-6.1.0.jre8.jar 및 mssql-jdbc-6.1.0.jre7.jar 파일을 빌드합니다.

## <a name="60"></a>6.0

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 6.0(자동 압축 풀기 exe) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122617)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 6.0(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122714)**  

버전 번호: 6.0.8112  
릴리스 날짜: 2017년 1월 17일

검색된 언어가 아닌 다른 언어로 드라이버를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
자동 압축 풀기 exe 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x40a)  
tar.gz 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x40a)  

SQL Server용 Microsoft JDBC Driver 6.0은 JDBC API 사양 4.1 및 4.2를 완벽하게 준수합니다. 6\.0 패키지의 jar는 JDBC API 버전에 따라 이름이 지정됩니다. 예를 들어 6.0 패키지의 sqljdbc42.jar는 JDBC API 4.2를 준수합니다. 마찬가지로 sqljdbc41.jar 파일은 JDBC API 4.1을 준수합니다.

적절한 sqljdbc42.jar 또는 sqljdbc41.jar 파일이 있는지 확인하려면 다음 코드 줄을 실행합니다. 출력이 "드라이버 버전: 6.0.7507.100"인 경우 JDBC 드라이버 6.0 패키지가 있음을 의미합니다.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

이 드라이버는 SQL Server 2016에서 Always Encrypted 기능을 지원합니다. 이 기능을 사용하면 SQL Server 인스턴스에서 중요한 데이터가 일반 텍스트로 표시되지 않도록 할 수 있습니다. 항상 암호화는 SQL Server에서 일반 텍스트 값이 아니라 암호화된 데이터만 처리하도록 애플리케이션의 데이터를 투명하게 암호화하여 작동합니다. SQL Server 인스턴스 또는 호스트 머신이 손상된 경우에도 공격자가 얻을 수 있는 것은 중요한 데이터의 암호 텍스트뿐입니다. 자세한 내용은 [Always Encrypted와 JDBC Driver 사용](using-always-encrypted-with-the-jdbc-driver.md)을 참조하세요.

### <a name="internationalized-domain-names"></a>다국어 도메인 이름

이 드라이버에서는 서버 이름에 IDN(다국어 도메인 이름)을 지원합니다. 자세한 내용은 [International features of the JDBC Driver](international-features-of-the-jdbc-driver.md)(JDBC Driver의 국가별 기능) 문서에서 "Using International Domain Names(다국어 도메인 이름 사용)"를 참조하세요.

### <a name="parameterized-queries"></a>매개 변수가 있는 쿼리

이제 드라이버는 하위 쿼리 및/또는 조인과 같은 복합 쿼리를 위해 준비된 문을 사용하여 매개 변수 메타데이터를 검색할 수 있도록 지원합니다. 이러한 향상 기능은 SQL Server 2012 및 최신 버전을 사용하는 경우에만 사용할 수 있습니다.

### <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 인증은 Azure AD에서 ID를 참조하여 Azure SQL Database v12에 연결하는 메커니즘입니다. 중앙에서 데이터베이스 사용자의 ID를 관리할 수 있는 Azure AD 인증은 SQL Server 인증 대신으로도 사용할 수 있습니다.

JDBC Driver 6.0을 사용하면 JDBC 연결 문자열에서 Azure AD 자격 증명을 지정하여 Azure SQL Database에 연결할 수 있습니다. 자세한 내용은 [연결 속성 설정](setting-the-connection-properties.md) 문서의 authentication 속성을 참조하세요.

### <a name="table-valued-parameters"></a>테이블 반환 매개 변수

TVP를 사용하면 데이터를 처리하는 데 여러 번 왕복하거나 서버 측 특수 논리를 설정하지 않고도 데이터의 여러 행을 클라이언트 애플리케이션에서 SQL Server로 쉽게 마샬링할 수 있습니다. 또한 TVP를 사용하면 클라이언트 애플리케이션에서 데이터 행을 캡슐화하고 매개 변수가 있는 단일 명령으로 데이터를 서버에 보낼 수 있습니다. 들어오는 데이터 행을 테이블 변수에 저장하여 Transact-SQL에서 사용할 수 있습니다. 자세한 내용은 [Using table-valued parameters](using-table-valued-parameters.md)(테이블 반환 매개 변수 사용)를 참조하세요.

### <a name="always-on-availability-groups"></a>Always On 가용성 그룹

이제 드라이버에서는 Always On 가용성 그룹에 투명하게 연결할 수 있습니다. 또한 서버 인프라의 현재 Always On 토폴로지를 신속히 검색하여 현재 활성 서버에 투명하게 연결됩니다.

## <a name="42"></a>4.2

**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 4.2(자동 압축 풀기 exe) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122538)**  
**[![다운로드](../../ssms/media/download-icon.png) SQL Server용 Microsoft JDBC Driver 4.2(tar.gz) 다운로드](https://go.microsoft.com/fwlink/?linkid=2122437)**  

버전 번호: 4.2.8112  
릴리스 날짜: 2015년 8월 24일

검색된 언어가 아닌 다른 언어로 드라이버를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
자동 압축 풀기 exe 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x40a)  
tar.gz 파일에 포함된 드라이버: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x40a)  

SQL Server용 Microsoft JDBC Driver 4.2는 JDBC API 사양 4.1 및 4.2를 완벽하게 준수합니다. 4\.2 패키지의 jar는 JDBC API 버전에 따라 이름이 지정됩니다. 예를 들어 4.2 패키지의sqljdbc42.jar 파일은 JDBC API 4.2를 준수합니다. 마찬가지로 sqljdbc41.jar 파일은 JDBC API 4.1을 준수합니다.

적절한 sqljdbc42.jar 또는 sqljdbc41.jar 파일이 있는지 확인하려면 다음 코드 줄을 실행합니다. 출력이 "드라이버 버전: 4.2.6420.100"인 경우 JDBC 드라이버 4.2 패키지가 있음을 의미합니다.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>JDK 8 지원

이 드라이버에서는 JDK 7.0, 6.0 및 5.0 외에도 JDK 버전 8.0을 지원합니다.

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 및 4.2 준수

드라이버는 4.0 외에도 Java Database Connectivity API 4.1 및 4.2 사양을 지원합니다. 자세한 내용은 [JDBC 4.1 compliance for the JDBC Driver](jdbc-4-1-compliance-for-the-jdbc-driver.md)(JDBC Driver의 JDBC 4.1 준수) 및 [JDBC 4.2 compliance for the JDBC Driver](jdbc-4-2-compliance-for-the-jdbc-driver.md)(JDBC Driver의 JDBC 4.2 준수)를 참조하세요.

### <a name="bulk-copy"></a>대량 복사

대량 복사 기능을 사용하여 SQL Server 데이터베이스의 테이블이나 뷰에 많은 양의 데이터를 신속하게 복사할 수 있습니다. 자세한 내용은 [JDBC Driver에서 대량 복사 사용](using-bulk-copy-with-the-jdbc-driver.md)을 참조하세요.

### <a name="xa-transaction-rollback-option"></a>XA 트랜잭션 롤백 옵션

드라이버에 이제 준비되지 않은 트랜잭션의 기존 자동 롤백에 대해 새로운 제한 시간 옵션이 있습니다. 자세한 내용은 [Understanding XA transactions](understanding-xa-transactions.md)(XA 트랜잭션이해)를 참조하세요.

### <a name="new-kerberos-principal-connection-property"></a>새 Kerberos 보안 주체 연결 속성

드라이버는 새 연결 속성을 사용하여 Kerberos 연결을 유연하게 합니다. 자세한 내용은 [Kerberos 통합 인증을 사용하여 SQL Server에 연결](using-kerberos-integrated-authentication-to-connect-to-sql-server.md)을 참조하세요.

## <a name="41"></a>4.1

버전 번호: 4.1.8112  
릴리스 날짜: 2014년 12월 12일

### <a name="support-for-jdk-7"></a>JDK 7 지원

이 드라이버에서는 JDK 6.0 및 5.0 외에도 JDK 버전 7.0을 지원합니다.

## <a name="itanium-not-supported-for-jdbc-driver-applications"></a>Itaniu에서는 JDBC 드라이버 애플리케이션이 지원되지 않음

SQL Server 애플리케이션용 Microsoft JDBC Driver는 Itanium 컴퓨터에서 실행할 수 없습니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 개요](overview-of-the-jdbc-driver.md)
