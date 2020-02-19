---
title: '2단원: 연결 정보 지정(Reporting Services) | Microsoft Docs'
description: 이 단원에서는 보고서에서 관계형 데이터베이스 또는 다른 원본의 데이터에 액세스하는 데 사용하는 연결 정보 및 데이터 원본을 정의합니다.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9d4e12a0322a35e96bd930c4fa6f1f852daf2bdd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75258460"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>2단원: 연결 정보 지정(Reporting Services)

1단원에서는 [!INCLUDE[ssrsnoversion-md](../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서를 Tutorial 프로젝트에 추가했습니다.
  
이 단원에서는 보고서에서 관계형 데이터베이스 또는 다른 원본의 데이터에 액세스하는 데 사용하는 연결 정보 및 데이터 원본을 정의해 보겠습니다. 

이 보고서에 대한 데이터 원본으로 AdventureWorks2016 샘플 데이터베이스를 추가하겠습니다. 이 자습서에서는 데이터베이스가 로컬 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]의 기본 인스턴스에 있다고 가정합니다.  

## <a name="to-set-up-a-connection"></a>연결을 설정하려면  

1. **보고서 데이터** 창에서 **새로 만들기** > **데이터 원본**을 선택합니다. **보고서 데이터** 창이 표시되지 않는 경우 **보기** 메뉴 > **보고서 데이터**를 선택합니다.

    ![ssrs-table-tutorial-2-new-data-source](media/ssrs-table-tutorial-2-new-data-source.png)

    **데이터 원본 속성** 대화 상자가 열리고 **일반** 섹션이 표시됩니다.

    ![데이터 원본 속성 대화 상자](media/lesson-2-specifying-connection-information-reporting-services/vs-datasource-connection-properties-dialog-box.png)

2. **이름** 텍스트 상자에 “AdventureWorks2016”을 입력합니다.

3. **포함된 연결** 라디오 단추를 선택합니다.

4. **형식** 드롭다운 선택 상자에서 “Microsoft SQL Server”를 선택합니다.
  
5. **연결 문자열** 텍스트 상자에 다음 문자열을 입력합니다.

    `Data source=localhost; initial catalog=AdventureWorks2016`

    > [!NOTE]
    > 이 연결 문자열에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], 보고서 서버 및 AdventureWorks2016 데이터베이스가 모두 로컬 컴퓨터에 설치되어 있다고 가정합니다.
    >
    >이 가정이 true가 아니면 연결 문자열을 변경하고 “localhost”를 데이터베이스 서버/인스턴스 이름으로 바꿉니다. [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 또는 SQL Server 명명된 인스턴스를 사용하는 경우 인스턴스 정보를 포함하도록 연결 문자열을 수정해야 합니다. 다음은 그 예입니다.
    >
    > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2016`
    >
    > 연결 문자열에 대한 자세한 내용은 아래 `See also` 섹션을 참조하세요.

6. **자격 증명** 탭을 선택하고, **데이터 원본에 연결하는 데 사용되는 자격 증명을 변경하세요.** 섹션 아래에서 **Windows 인증 사용(통합 보안)** 라디오 단추를 선택합니다.

7. **확인**을 선택하여 프로세스를 완료합니다.

보고서 디자이너의 **보고서 데이터** 창에 데이터 원본 AdventureWorks2016이 추가됩니다.

![ssrs-adventureworks-datasource](media/lesson-2-specifying-connection-information-reporting-services/ssrs-adventureworks-datasource2016.png)

## <a name="next-steps"></a>다음 단계

이 단원에서는 AdventureWorks2016 샘플 데이터베이스에 대한 연결을 성공적으로 정의했습니다. [3단원: 테이블 보고서에 대한 데이터 세트 정의 &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)를 계속 진행하여 보고서에 대한 데이터 세트를 정의하세요.

## <a name="see-also"></a>참고 항목

[데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)
