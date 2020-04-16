---
title: Integration Services(SSIS)에 대한 Azure 기능 팩 | Microsoft Docs
ms.custom: ''
ms.date: 12/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5099b46b611043dcbfa0f5b4c3ca4e72c70a5800
ms.sourcegitcommit: 52925f1928205af15dcaaf765346901e438ccc25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2020
ms.locfileid: "80607869"
---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Integration Services에 대한 Azure 기능 팩(SSIS)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Azure용 SSIS(SQL Server Integration Services) 기능 팩은 Azure 서비스에 연결하고, Azure 및 온-프레미스 데이터 원본 간에 데이터를 전송하고, Azure에 저장된 데이터를 처리하기 위해 SSIS에 이 페이지에 나열된 구성 요소를 제공하는 확장 프로그램입니다.

[![Azure용 SSIS 기능 팩 다운로드](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/download/details.aspx?id=100430) **다운로드**

- SQL Server 2019의 경우 - [Azure용 Microsoft SQL Server 2019 Integration Services 기능 팩](https://www.microsoft.com/download/details.aspx?id=100430)
- SQL Server 2017의 경우 - [Azure용 Microsoft SQL Server 2017 Integration Services 기능 팩](https://www.microsoft.com/download/details.aspx?id=54798)
- SQL Server 2016의 경우 - [Azure용 Microsoft SQL Server 2016 Integration Services 기능 팩](https://www.microsoft.com/download/details.aspx?id=49492)
- SQL Server 2014의 경우 - [Azure용 Microsoft SQL Server 2014 Integration Services 기능 팩](https://www.microsoft.com/download/details.aspx?id=47366)
- SQL Server 2012의 경우 - [Azure용 Microsoft SQL Server 2012 Integration Services 기능 팩](https://www.microsoft.com/download/details.aspx?id=47367)

다운로드 페이지도 필수 구성 요소에 대한 정보를 포함합니다. 서버에 Azure 기능 팩을 설치하기 전에 SQL Server가 설치되었는지 또는 서버에서 SSIS 카탈로그 데이터베이스인 SSISDB에 패키지를 배포할 때 기능 팩의 구성 요소를 사용할 수 없는지 확인합니다.

## <a name="components-in-the-feature-pack"></a>기능 팩의 구성 요소
-   연결 관리자

    -   [Azure Data Lake Analytics 연결 관리자](connection-manager/azure-data-lake-analytics-connection-manager.md)

    -   [Azure Data Lake Store 연결 관리자](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Azure HDInsight 연결 관리자](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

    -   [Azure Resource Manager 연결 관리자](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Azure Storage 연결 관리자](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure 구독 연결 관리자](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
-   작업

    -   [Azure Blob 다운로드 작업](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure Blob 업로드 태스크](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Data Lake Analytics 태스크](control-flow/azure-data-lake-analytics-task.md)

    -   [Azure Data Lake Store 파일 시스템 태스크](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

    -   [Azure HDInsight 클러스터 만들기 태스크](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight 클러스터 삭제 작업](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure HDInsight 하이브 태스크](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig 태스크](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure SQL DW 업로드 태스크](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Flexible File 태스크](../integration-services/control-flow/flexible-file-task.md)

-   데이터 흐름 구성 요소

    -   [Azure Blob 원본](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob 대상](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store 원본](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 대상](../integration-services/data-flow/azure-data-lake-store-destination.md)

    -   [Flexible File 원본](../integration-services/data-flow/flexible-file-source.md)

    -   [Flexible File 대상](../integration-services/data-flow/flexible-file-destination.md)

-   Azure Blob, Azure Data Lake Store 및 Data Lake Storage Gen2 파일 열거자 [Foreach 루프 컨테이너](../integration-services/control-flow/foreach-loop-container.md)를 참조하세요.

## <a name="use-tls-12"></a>TLS 1.2 사용

Azure 기능 팩에서 사용하는 TLS 버전은 시스템 .NET Framework 설정을 따릅니다.
TLS 1.2를 사용하려면 다음 두 개의 레지스트리 키 아래에 데이터가 `1`인 `SchUseStrongCrypto`라는 `REG_DWORD` 값을 추가합니다.

1. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319`

## <a name="dependency-on-java"></a>Java에 대한 종속성

Java는 Azure Data Lake Store/유연한 파일 커넥터에 ORC/Parquet 파일 형식을 사용해야 합니다.  
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

> [!TIP]
> Parquet 형식을 사용하고 "Java를 호출할 때 오류가 발생했습니다. 메시지: **java.lang.OutOfMemoryError:Java heap space**"라는 오류가 발생하는 경우 환경 변수 *`_JAVA_OPTIONS`* 를 추가하여 JVM의 최소/최대 힙 크기를 조정할 수 있습니다.
>
>![jvm heap](media/azure-feature-pack-jvm-heap-size.png)
>
> 예: 변수 *`_JAVA_OPTIONS`* 를 *`-Xms256m -Xmx16g`* 값으로 설정합니다. 플래그 Xms는 JVM(Java Virtual Machine)의 초기 메모리 할당 풀을 지정하고, Xmx는 최대 메모리 할당 풀을 지정합니다. 즉, JVM은 *`Xms`* 의 메모리 양으로 시작하고 최대 *`Xmx`* 의 메모리 양을 사용할 수 있음을 의미합니다. 기본값은 최소 64MB, 최대 1G입니다.

### <a name="set-up-zulus-openjdk-on-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime에서 Zulu OpenJDK 설정

이 작업은 Azure-SSIS Integration Runtime에 대한 [사용자 지정 설정 인터페이스](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)를 통해 수행해야 합니다.
`zulu8.33.0.1-jdk8.0.192-win_x64.zip`을 사용한다고 가정합니다.
Blob 컨테이너는 다음과 같이 구성할 수 있습니다.

~~~
main.cmd
install_openjdk.ps1
zulu8.33.0.1-jdk8.0.192-win_x64.zip
~~~

진입 점으로 `main.cmd` 는 PowerShell 스크립트 `install_openjdk.ps1`의 실행을 트리거하여 `zulu8.33.0.1-jdk8.0.192-win_x64.zip`을 추출하고 이에 따라 `JAVA_HOME`을 설정합니다.

**main.cmd**

~~~
powershell.exe -file install_openjdk.ps1
~~~

> [!TIP]
> Parquet 형식을 사용하고 "Java를 호출할 때 오류가 발생했습니다. 메시지: **java.lang.OutOfMemoryError:Java heap space**"라는 오류가 발생하는 경우 *`main.cmd`* 명령을 추가하여 JVM의 최소/최대 힙 크기를 조정할 수 있습니다. 예제:
> ~~~
> setx /M _JAVA_OPTIONS "-Xms256m -Xmx16g"
> ~~~
> 플래그 Xms는 JVM(Java Virtual Machine)의 초기 메모리 할당 풀을 지정하고, Xmx는 최대 메모리 할당 풀을 지정합니다. 즉, JVM은 *`Xms`* 의 메모리 양으로 시작하고 최대 *`Xmx`* 의 메모리 양을 사용할 수 있음을 의미합니다. 기본값은 최소 64MB, 최대 1G입니다.

**install_openjdk.ps1**

~~~
Expand-Archive zulu8.33.0.1-jdk8.0.192-win_x64.zip -DestinationPath C:\
[Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\zulu8.33.0.1-jdk8.0.192-win_x64\jre", "Machine")
~~~

### <a name="set-up-oracles-java-se-runtime-environment"></a>Oracle Java SE Runtime Environment 설치

1. exe 설치 관리자를 다운로드하여 실행합니다.
2. 설치 관리자 지침에 따라 설치를 완료합니다.

## <a name="scenario-processing-big-data"></a>시나리오: 빅 데이터 처리
 Azure 커넥터를 사용하여 다음과 같은 빅 데이터 처리 작업을 완료합니다.

1.  Azure Blob 업로드 태스크를 사용하여 Azure Blob Storage에 입력 데이터를 업로드합니다.

2.  Azure HDInsight 클러스터 만들기 태스크를 사용하여 Azure HDInsight 클러스터를 만듭니다. 자체 클러스터를 사용하려는 경우 이 단계는 선택 사항입니다.

3.  Azure HDInsight Hive 태스크 또는 Azure HDInsight Pig 태스크를 사용하여 Azure HDInsight 클러스터에서 Pig 또는 Hive 작업을 호출합니다.

4.  2단계에서 주문형 HDInsight 클러스터를 만든 경우 Azure HDInsight 클러스터 삭제 태스크를 사용하여 사용한 HDInsight 클러스터를 삭제합니다.

5.  Azure HDInsight Blob 다운로드 태스크를 사용하여 Azure Blob Storage에서 Pig/Hive 출력 데이터를 다운로드합니다.

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>시나리오: 클라우드의 데이터 관리
 SSIS 패키지의 Azure Blob 대상을 사용하여 Azure Blob Storage에 출력 데이터를 쓰거나 Azure Blob 원본을 사용하여 Azure Blob Storage에서 데이터를 읽습니다.

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 Azure Blob 열거자에서 Foreach 루프 컨테이너를 사용하여 다중 blob 파일의 데이터를 처리합니다.

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)

## <a name="release-notes"></a>릴리스 정보

### <a name="version-1180"></a>버전 1.18.0

#### <a name="improvements"></a>개선 사항

1. 유연한 파일 작업을 위한 다음 세 가지 개선 사항이 있습니다. (1) 복사/삭제 작업에 대한 와일드카드 지원이 추가되었습니다. (2) 사용자가 삭제 작업을 위한 재귀 검색을 사용하거나 사용하지 않도록 설정할 수 있습니다. (3) 원본 파일 이름을 유지하기 위해 복사 작업의 대상 파일 이름을 비워 둘 수 있습니다.

### <a name="version-1170"></a>버전 1.17.0

SQL Server 2019에 대해서만 릴리스된 핫픽스 버전입니다.

#### <a name="bugfixes"></a>버그 수정

1. Visual Studio 2019에서 SQL Server 2019를 대상으로 실행하는 경우 유연한 파일 작업/원본/대상이 실패하고 다음 오류 메시지가 표시될 수 있습니다. `Attempted to access an element as a type incompatible with the array.`
1. Visual Studio 2019에서 SQL Server 2019를 대상으로 실행하는 경우 ORC/Parquet 형식을 사용한 유연한 파일 원본/대상이 실패하고 다음 오류 메시지가 표시될 수 있습니다. `Microsoft.DataTransfer.Common.Shared.HybridDeliveryException: An unknown error occurred. JNI.JavaExceptionCheckException.`

### <a name="version-1160"></a>버전 1.16.0

#### <a name="bugfixes"></a>버그 수정

1. 경우에 따라 패키지 실행 보고서에서 "오류: "파일이나 어셈블리 'Newtonsoft.Json, Version=11.0.0.0, Culture=neutral, PublicKeyToken=30ad4fe6b2a6aeed' 또는 여기에 종속되어 있는 파일이나 어셈블리 중 하나를 로드할 수 없습니다.”를 보고합니다.

### <a name="version-1150"></a>버전 1.15.0

#### <a name="improvements"></a>개선 사항

1. Flexible File 태스크에 폴더/파일 삭제 작업 추가
1. Flexible File 원본에서 외부/출력 데이터 형식 변환 함수 추가

#### <a name="bugfixes"></a>버그 수정

1. 경우에 따라 "배열과 호환되지 않는 형식으로 요소를 액세스하려고 했습니다"라는 오류 메시지와 함께 Data Lake Storage Gen2에 대한 연결 테스트가 오작동합니다.
1. Azure Storage 에뮬레이터에 대한 지원 재개
