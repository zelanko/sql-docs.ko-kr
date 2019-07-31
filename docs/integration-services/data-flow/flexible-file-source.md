---
title: 유연한 파일 원본 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpextfilesrc.f1
- sql14.dts.designer.afpextfilesrc.f1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 277c688b77e74d1dad35b19c279a648e56b8f396
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316674"
---
# <a name="flexible-file-source"></a>유연한 파일 원본

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

**Flexible File Source** 구성 요소를 사용하면 SSIS 패키지가 지원되는 여러 스토리지 서비스에서 데이터를 읽을 수 있습니다.
현재 지원되는 스토리지 서비스는 다음과 같습니다.

- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)
  
Flexible File Source용 편집기를 표시하려면 데이터 흐름 디자이너에서 **Flexible File Source**를 끌어서 놓고 두 번 클릭하여 편집기를 엽니다.
  
**Flexible File Source**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.  
  
**유연한 파일 원본 편집기**에서 다음 속성을 사용할 수 있습니다.

- **파일 연결 관리자 유형:** 원본 연결 관리자 유형을 지정합니다. 그런 다음, 지정된 형식의 기존 항목을 선택하거나 새로 만듭니다.
- **폴더 경로:** 원본 폴더 경로를 지정합니다.
- **파일 이름:** 원본 파일 이름을 지정합니다.
- **파일 형식:** 원본 파일 형식을 지정합니다. 지원 되는 형식은 **텍스트**, **Avro**, **ORC**, **Parquet**입니다.
- **열 구분 기호 문자:** 열 구분 기호로 사용할 문자를 지정합니다(다중 문자 구분 기호 지원 안 함).
- **첫 행은 열 이름으로:** 첫 번째 행을 열 이름으로 간주할 것인지 여부를 지정합니다.
- **파일 압축 풀기:** 원본 파일의 압축을 풀지 여부를 지정합니다.
- **압축 유형:** 원본 파일 압축 형식을 지정합니다. 지원되는 형식은 **GZIP**, **DEFLATE**, **BZIP2**입니다.
  
**고급 편집기**에서 다음 속성을 사용할 수 있습니다.

- **rowDelimiter:** 파일의 행을 구분하는 데 사용되는 문자입니다. 하나의 문자만 허용됩니다. **기본**값은 \r\n입니다.
- **escapeChar:** 입력 파일의 내용에서 열 구분 기호를 이스케이프하는 데 사용되는 특수 문자입니다. 테이블에 escapeChar와 quoteChar를 둘 다 지정할 수 없습니다. 하나의 문자만 허용됩니다. 기본값이 없습니다.
- **quoteChar:** 문자열 값을 인용하는 데 사용되는 문자입니다. 인용 문자 안의 열과 행 구분 기호는 문자열 값의 일부로 처리됩니다. 이 속성은 입력 및 출력 데이터 세트 모두에 적용할 수 있습니다. 테이블에 escapeChar와 quoteChar를 둘 다 지정할 수 없습니다. 하나의 문자만 허용됩니다. 기본값이 없습니다.
- **nullValue:** null 값을 나타내는 데 사용되는 하나 이상의 문자입니다. **기본**값은 \N입니다.
- **encodingName:** 인코딩 이름을 지정합니다. [Encoding.EncodingName](https://docs.microsoft.com/dotnet/api/system.text.encoding?redirectedfrom=MSDN&view=netframework-4.8) 속성을 참조하세요.
- **skipLineCount:**  입력 파일에서 데이터를 읽을 때 건너뛸 비어 있지 않은 행의 수를 나타냅니다. skipLineCount와 firstRowAsHeader가 모두 지정되면 먼저 줄을 건너뛴 다음, 입력 파일에서 헤더 정보를 읽습니다.
- **treatEmptyAsNull:** 입력 파일에서 데이터를 읽을 때 null 또는 빈 문자열을 null 값으로 처리할지 여부를 지정합니다. **기본**값은 True입니다.

연결 정보를 지정한 후 **열** 페이지로 전환하여 SSIS 데이터 흐름의 원본 열을 대상 열에 매핑합니다.

**서비스 사용자 권한 구성에 대한 참고 사항**

**테스트 연결**이 이뤄지려면(Blob Storage 또는 Data Lake Storage Gen2) 서비스 사용자에게 스토리지 계정에 대한 **Storage Blob 데이터 읽기 권한자** 역할을 하나 이상 할당해야 합니다.
이 작업은 [RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal)를 사용하여 수행됩니다.

Blob Storage의 경우 최소한 **Storage Blob 데이터 읽기 권한자** 역할을 할당하여 읽기 권한을 부여합니다.

Data Lake Storage Gen2의 경우 RBAC 및 [ACL](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer)을 통해 사용 권한이 결정됩니다.
ACL은 [여기](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal)에 자세히 설명된 대로 앱 등록에 서비스 사용자의 OID(개체 ID)를 사용하여 구성된다는 것에 주의합니다.
RBAC 구성에 사용되는 애플리케이션(클라이언트) ID와는 다릅니다.
기본 제공 역할 또는 사용자 지정 역할을 통해 보안 주체에 RBAC 데이터 권한이 부여된 경우 요청의 권한 부여 시 먼저 이러한 사용 권한이 평가됩니다.
보안 주체의 RBAC 할당을 통해 요청한 작업의 권한이 부여된 경우 권한 부여가 즉시 확인되고 추가 ACL 검사가 수행되지 않습니다.
또는 보안 주체에 RBAC 할당이 없거나 요청한 작업이 할당된 사용 권한과 일치하지 않는 경우 ACL 검사를 통해 보안 주체가 요청된 작업을 수행할 수 있는 권한이 있는지 확인합니다.
읽기 권한의 경우 읽을 파일에 대한 **읽기** 권한과 함께 원본 파일 시스템부터 최소한 **실행** 권한을 부여합니다.
또는 RBAC를 사용하여 최소한 **Storage Blob 데이터 읽기 권한자** 역할을 부여합니다.
자세한 내용은 [이](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control) 문서를 참조하세요.

**ORC/Parquet 파일 형식의 필수 구성 요소**

Java는 ORC/Parquet 파일 형식을 사용해야 합니다.
Java 빌드의 아키텍처(32/64비트)는 사용할 SSIS 런타임과 일치해야 합니다.
다음과 같은 Java 빌드가 테스트되었습니다.

- [Zulu OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

**Zulu OpenJDK 설치**

1. zip 패키지를 다운로드하여 추출합니다.
2. 명령 프롬프트에서 `sysdm.cpl`을 실행합니다.
3. **고급** 탭에서 **환경 변수**를 선택합니다.
4. **시스템 변수** 섹션 아래에서 **새로 만들기**를 선택합니다.
5. **변수 이름**에 대해 `JAVA_HOME`을 입력합니다.
6. **디렉터리 찾아보기**를 선택하여 추출된 폴더로 이동하고, `jre` 하위 폴더를 선택합니다.
   그런 다음, **확인**을 선택하면 **변수 값**이 자동으로 채워집니다.
7. **확인**을 선택하여 **새 시스템 변수** 대화 상자를 닫습니다.
8. **확인**을 선택하여 **환경 변수** 대화 상자를 닫습니다.
9. **확인**을 선택하여 **시스템 속성** 대화 상자를 닫습니다.

**Oracle Java SE Runtime Environment 설치**

1. exe 설치 관리자를 다운로드하여 실행합니다.
2. 설치 관리자 지침에 따라 설치를 완료합니다.
