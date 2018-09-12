---
title: DAC 패키지 압축 풀기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- wizard [DAC], unpack
- data-tier application [SQL Server], unpack
- How to [DAC], unpack
- unpack DAC
ms.assetid: 697b69b3-f157-4e22-ac4e-f65c5fc2d0ad
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d256a069213df774519a357d29ab1be8fe5417d8
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809669"
---
# <a name="unpack-a-dac-package"></a>DAC 패키지 압축 풀기
  데이터 계층 응용 프로그램 압축 풀기 대화 상자를 사용하여 DAC(데이터 계층 응용 프로그램) 패키지에서 스크립트와 파일 압축을 해제할 수 있습니다. 스크립트와 파일은 폴더에 저장되며 패키지를 사용하여 DAC를 프로덕션 시스템에 배포하기 전에 폴더에서 검토할 수 있습니다. 한 DAC의 내용을 다른 폴더에 압축을 푼 다른 패키지의 내용과 비교할 수도 있습니다.  
  
1.  **시작하기 전 주의 사항:**  [보안](#Security)  
  
2.  **DAC 압축을 풀려면:**  [데이터 계층 응용 프로그램 압축 풀기 대화 상자](#UnpackDACDial), [DAC 패키지의 내용 검사](#ExamDACPack)  
  
##  <a name="Security"></a> 보안  
 출처를 알 수 없거나 신뢰할 수 없는 DAC 패키지는 배포하지 않는 것이 좋습니다. 이러한 DAC에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마를 수정하여 오류가 발생할 수 있습니다. 출처를 알 수 없거나 신뢰할 수 없는 DAC를 사용하려면 먼저 격리된 테스트 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 배포하고 DAC 압축을 푼 다음 저장 프로시저나 다른 사용자 정의 코드와 같은 코드를 검사하십시오.  
  
##  <a name="UnpackDACDial"></a> 데이터 계층 응용 프로그램 압축 풀기 대화 상자  
 **DAC 패키지 파일을 압축을 풀려면**  
  
-   **Windows 탐색기**에서 DAC 패키지(.dacpac) 파일의 위치로 이동합니다.  
  
-   다음 두 가지 방법 중 하나를 사용하여 데이터 계층 응용 프로그램 압축 풀기 대화 상자를 엽니다.  
  
    1.  DAC 패키지(.dacpac) 파일을 마우스 오른쪽 단추로 클릭하고 **압축 풀기**를 선택합니다.  
  
    2.  DAC 패키지 파일을 두 번 클릭합니다.  
  
-   대화 상자를 완료합니다.  
  
    -   [Microsoft SQL Server DAC 패키지 파일 압축 풀기](#Unpack)  
  
    -   [폴더 찾아보기](#Browse)  
  
###  <a name="Unpack"></a> Microsoft SQL Server DAC 패키지 파일 압축 풀기  
 이 페이지를 사용하여 파일 압축을 풀 대상 폴더를 지정하고 압축 풀기 작업을 실행할 수 있습니다.  
  
 **다음 폴더에 파일 압축 풀기:** - 파일 압축을 풀 폴더의 전체 경로를 지정합니다. 폴더가 존재하고 전체 경로를 아는 경우 입력란에 경로를 입력합니다. 그렇지 않으면 **찾아보기** 단추를 클릭하여 폴더로 이동하거나 새 폴더를 만듭니다.  
  
 **찾아보기** - 파일 계층을 탐색하거나 새 폴더를 만들어 폴더를 선택할 수 있는 **폴더 찾아보기** 페이지를 엽니다.  
  
 **압축 풀기** - 압축 풀기 작업을 시작합니다.  
  
 **취소** - DAC 패키지 압축을 풀지 않고 대화 상자를 종료합니다.  
  
###  <a name="Browse"></a> 폴더 찾아보기  
 이 페이지를 사용하여 압축 풀기 작업의 대상 폴더를 선택할 수 있습니다. 필요에 따라 새 폴더를 만들 수도 있습니다.  
  
 **폴더 목록** - 컴퓨터의 파일 계층을 표시합니다. 노드를 확장하여 DAC 패키지 압축을 풀 폴더로 이동합니다. 폴더를 클릭한 다음 **확인**을 클릭합니다.  
  
 **새 폴더 만들기** - 폴더 계층에서 현재 선택된 폴더에 생성될 새 폴더의 이름을 지정할 수 있는 대화 상자를 엽니다.  
  
 **확인** - **DAC 패키지 파일 압축 풀기** 페이지의 **다음 폴더에 파일 압축 풀기** 입력란에 선택되어 있는 폴더에 대한 경로를 적용하고 해당 페이지로 돌아갑니다.  
  
 **취소** - 폴더를 선택하지 않고 대화 상자를 종료합니다.  
  
##  <a name="ExamDACPack"></a> DAC 패키지의 내용 검사  
 패키지의 압축을 푼 후에는 **데이터 계층 응용 프로그램 압축 풀기** 대화 상자에서 생성한 파일을 검사할 수 있습니다. 대화 상자는 선택된 대상 폴더에 다음 파일을 작성합니다.  
  
1.  DAC에 정의된 개체를 생성하는 문을 포함하는 Transact-SQL 스크립트. 파일 이름은 *DACName*.sql이며 *DACName* 은 DAC의 이름입니다.  
  
2.  패키지의 모든 XML 파일  
  
3.  DAC 배포 전 또는 배포 후 파일과 같은 DAC의 여분 파일에 있는 모든 파일  
  
 자세한 내용은 [Validate a DAC Package](validate-a-dac-package.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 계층 응용 프로그램](data-tier-applications.md)   
 [데이터 계층 응용 프로그램 배포](deploy-a-data-tier-application.md)   
 [데이터 계층 응용 프로그램 업그레이드](upgrade-a-data-tier-application.md)  
  
  
