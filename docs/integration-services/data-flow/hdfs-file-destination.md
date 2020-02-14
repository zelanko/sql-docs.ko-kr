---
title: HDFS 파일 대상 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eec72a0421576ed4c09d35cd19bb0d842bd08f78
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71292369"
---
# <a name="hdfs-file-destination"></a>HDFS 파일 대상

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SSIS 패키지는 HDFS 파일 대상 구성 요소를 통해 HDFS 파일에 데이터를 쓸 수 있습니다. 지원되는 파일 형식은 텍스트, Avro 및 ORC입니다.

 HDFS 파일 대상을 구성하려면 데이터 흐름 디자이너에서 HDFS 파일 원본을 끌어서 놓은 다음 구성 요소를 두 번 클릭하여 편집기를 엽니다.

 ![HDFS 파일 대상 편집기](../../integration-services/data-flow/media/hdfs-file-dest.png "HDFS 파일 대상 편집기")

## <a name="options"></a>옵션
 **Hadoop 파일 대상 편집기** 대화 상자의 **일반** 탭에서 다음 옵션을 구성합니다.

|필드|Description|
|-----------|-----------------|
|**Hadoop 연결**|기존 Hadoop 연결 관리자를 지정하거나 새 연결 관리자를 만듭니다. 이 연결 관리자는 HDFS 파일이 호스트되는 위치를 나타냅니다.|
|**파일 경로**|HDFS 파일의 이름을 지정합니다.|
|**파일 형식**|HDFS 파일의 형식을 지정합니다. 사용할 수 있는 옵션은 텍스트, Avro, ORC입니다.|
|**열 구분 기호 문자**|텍스트 형식을 선택하는 경우 열 구분 기호 문자를 지정합니다.|
|**첫 번째 데이터 행의 열 이름**|텍스트 형식을 선택하는 경우 파일의 첫 행에 열 이름을 포함할지 여부를 지정합니다.|

 이러한 옵션을 구성한 후 **열** 탭을 선택하여 데이터 흐름에서 원본 열을 대상 열에 매핑합니다.

::: moniker range=">= sql-server-ver15"

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

::: moniker-end

## <a name="see-also"></a>참고 항목
[Hadoop 연결 관리자](../../integration-services/connection-manager/hadoop-connection-manager.md)  
[HDFS 파일 원본](../../integration-services/data-flow/hdfs-file-source.md)
