---
title: Azure Data Lake Store 대상 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e9ccc245c540cfa6e87ee13f6cbb09f10c7734b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045443"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 대상

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Azure Data Lake Store 대상** 구성 요소를 사용하면 SSIS 패키지가 Azure Data Lake Store에 데이터를 쓸 수 있습니다. 지원되는 파일 형식은 다음과 같습니다. 텍스트, Avro 및 ORC. 
  
 **Azure Data Lake Store 대상**은 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.
 
> [!NOTE]
> Azure Data Lake Store 연결 관리자와 이 연결 관리자를 사용하는 구성 요소(즉, Azure Data Lake Store 원본과 Azure Data Lake Store 대상)를 서비스에 연결하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 

## <a name="configure-the-azure-data-lake-store-destination"></a>Azure Data Lake Store 대상 구성  
1. **Azure Data Lake Store 대상** 을 데이터 흐름 디자이너에 끌어서 놓은 다음 두 번 클릭하여 편집기를 표시합니다.  

2.  **Azure Data Lake Store 연결 관리자** 필드에서는 기존 Azure Data Lake Store 연결 관리자를 지정하거나 Azure Data Lake Store 서비스를 참조하는 연결 관리자를 새로 만듭니다.  
  
    1.  **파일 경로** 필드에서는 데이터를 기록할 파일 이름을 지정합니다. 이 파일이 이미 있는 경우 해당 콘텐츠를 덮어씁니다.  
  
    2.  **파일 형식** 필드에서는 사용할 파일 형식을 지정합니다.  
  
       파일 형식이 Text이면 **열 구분 기호 문자** 값을 지정해야 합니다. 파일의 첫 행에 열 이름을 포함하려는 경우에는 **첫 번째 데이터 행의 열 이름** 도 선택합니다.  

       파일 형식이 ORC인 경우 올바른 플랫폼에 JRE(Java Runtime Environment)를 설치해야 합니다.
  
3.  연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.  

## <a name="prerequisite-for-orc-file-format"></a>ORC 파일 형식의 필수 구성 요소
Java는 ORC 파일 형식을 사용해야 합니다.
Java 빌드의 아키텍처(32/64비트)는 사용할 SSIS 런타임과 일치해야 합니다.
다음과 같은 Java 빌드가 테스트되었습니다.

- [Zulu OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Zulu OpenJDK 설치
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

### <a name="set-up-oracles-java-se-runtime-environment"></a>Oracle Java SE Runtime Environment 설치
1. exe 설치 관리자를 다운로드하여 실행합니다.
2. 설치 관리자 지침에 따라 설치를 완료합니다.