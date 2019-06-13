---
title: 유연한 파일 대상 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpextfiledest.f1
- sql14.dts.designer.afpextfiledest.f1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a0ffa4b881fe550aba6c547fcea690932eef110
ms.sourcegitcommit: fa2afe8e6aec51e295f55f8cc6ad3e7c6b52e042
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/03/2019
ms.locfileid: "66462618"
---
# <a name="flexible-file-destination"></a>유연한 파일 대상

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

**Flexible File Destination** 구성 요소를 사용하면 SSIS 패키지가 지원되는 여러 스토리지 서비스에 데이터를 쓸 수 있습니다.

현재 지원되는 스토리지 서비스는 다음과 같습니다.

- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)
   
**Flexible File Destination**을 데이터 흐름 디자이너에 끌어서 놓은 다음, 두 번 클릭하여 편집기를 표시합니다.
  
**Flexible File Destination**은 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.  

**유연한 파일 대상 편집기**에서 다음 속성을 사용할 수 있습니다.

- **파일 연결 관리자 유형:** 원본 연결 관리자 유형을 지정합니다. 그런 다음, 지정된 형식의 기존 항목을 선택하거나 새로 만듭니다.
- **폴더 경로:** 대상 폴더 경로를 지정합니다.
- **파일 이름:** 대상 파일 이름을 지정합니다.
- **파일 형식:** 대상 파일 형식을 지정합니다. 지원 되는 형식은 **텍스트**, **Avro**, **ORC**, **Parquet**입니다.
- **열 구분 기호 문자:** 열 구분 기호로 사용할 문자를 지정합니다(다중 문자 구분 기호 지원 안 함).
- **첫 행은 열 이름으로:** 첫 번째 행에 열 이름을 쓸 것인지 여부를 지정합니다.
- **파일 압축:** 파일을 압축할지 여부를 지정합니다.
- **압축 유형:** 사용할 압축 형식을 지정합니다. 지원되는 형식은 **GZIP**, **DEFLATE**, **BZIP2**입니다.
- **압축 수준:** 사용할 압축 수준을 지정합니다.

**고급 편집기**에서 다음 속성을 사용할 수 있습니다.

- **rowDelimiter:** 파일의 행을 구분하는 데 사용되는 문자입니다. 하나의 문자만 허용됩니다. **기본**값은 \r\n입니다.
- **escapeChar:** 입력 파일의 내용에서 열 구분 기호를 이스케이프하는 데 사용되는 특수 문자입니다. 테이블에 escapeChar와 quoteChar를 둘 다 지정할 수 없습니다. 하나의 문자만 허용됩니다. 기본값이 없습니다.
- **quoteChar:** 문자열 값을 인용하는 데 사용되는 문자입니다. 인용 문자 안의 열과 행 구분 기호는 문자열 값의 일부로 처리됩니다. 이 속성은 입력 및 출력 데이터 세트 모두에 적용할 수 있습니다. 테이블에 escapeChar와 quoteChar를 둘 다 지정할 수 없습니다. 하나의 문자만 허용됩니다. 기본값이 없습니다.
- **nullValue:** null 값을 나타내는 데 사용되는 하나 이상의 문자입니다. **기본**값은 \N입니다.
- **encodingName:** 인코딩 이름을 지정합니다. [Encoding.EncodingName](https://docs.microsoft.com/en-us/dotnet/api/system.text.encoding?redirectedfrom=MSDN&view=netframework-4.8) 속성을 참조하세요.
- **skipLineCount:**  입력 파일에서 데이터를 읽을 때 건너뛸 비어 있지 않은 행의 수를 나타냅니다. skipLineCount와 firstRowAsHeader가 모두 지정되면 먼저 줄을 건너뛴 다음, 입력 파일에서 헤더 정보를 읽습니다.
- **treatEmptyAsNull:** 입력 파일에서 데이터를 읽을 때 null 또는 빈 문자열을 null 값으로 처리할지 여부를 지정합니다. **기본**값은 True입니다.

연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.

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
