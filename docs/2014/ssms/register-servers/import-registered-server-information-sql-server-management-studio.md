---
title: 등록된 서버 정보 가져오기
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.importregisteredservers.f1
helpviewer_keywords:
- transferring registered server information
- Registered Servers [SQL Server], importing
- importing registered server information
ms.assetid: cc497a14-1360-4887-b70c-002f042823b6
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 32ef669c238c52ec5e5e20804c896b4364c8bc85
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75241346"
---
# <a name="import-registered-server-information-sql-server-management-studio"></a>등록된 서버 정보 가져오기(SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 저장된 등록된 서버 정보를 가져오는 방법에 대해 설명합니다. 등록된 서버 파일을 내보냈다가 다시 가져오면 등록된 서버에 있는 동일한 서버로 여러 컴퓨터를 쉽게 구성할 수 있습니다. 이 작업은 여러 곳에 위치한 컴퓨터에서 다수의 서버를 관리할 때나 경험이 적은 사용자를 위해 기본 연결 설정을 구성하려는 경우에 유용합니다.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에 등록된 서버 정보를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 가져올 수는 없습니다.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-import-registered-server-information"></a>등록된 서버 정보를 가져오려면  
  
1.  등록된 서버의 등록된 서버 도구 모음에서 해당 서버 유형을 클릭합니다. 서버 유형은 내보낸 파일의 등록된 서버 유형과 같아야 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 등록된 서버 정보를 내보낸 경우 등록된 서버 도구 모음에서 **SQL Server** 를 클릭해야 합니다.  
  
2.  서버 그룹을 마우스 오른쪽 단추로 클릭한 다음 **가져오기**를 선택합니다.  
  
3.  **등록된 서버 가져오기** 대화 상자에서 가져오려는 등록된 서버 파일을 선택한 다음 **확인**을 클릭합니다.  
  
     **파일 가져오기**  
     입력란에 가져올 파일 이름을 입력하거나 찾아보기 단추( **...** )를 클릭하여 클라이언트 컴퓨터에서 가져올 파일을 찾습니다. 기존 파일을 선택하면 등록된 서버 정보가 파일에 추가됩니다. 이전에 내보낸 등록된 서버 파일만 가져올 수 있습니다. 등록된 서버 파일의 확장자는 .regsrvr입니다.  
  
     **가져올 서버 그룹을 선택하세요.**  
     파일의 등록된 서버 항목을 가져올 루트 노드나 특정 서버 그룹을 선택합니다. 등록된 모든 서버, 특정 서버 그룹에 속한 등록된 서버 또는 등록된 단일 서버를 내보내기 파일로 가져올 수 있습니다. 가져오기 기능은 재귀적입니다. 예를 들어 서버 그룹 A에는 서버 그룹 B가, 서버 그룹 B에는 서버 그룹 C와 D가 포함된 경우 서버 그룹 A를 가져오면 A, B, C, D의 모든 항목이 내보내집니다.  
  
     서버 그룹은 현재 등록된 서버 트리의 서버 그룹만 표시합니다.  
  
     기존 서버 그룹이나 서버를 가져오도록 선택하면 기존 서버나 서버 그룹을 덮어쓸지 확인하는 메시지가 나타납니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 서버 등록은 사용자 단위로 암호를 저장합니다. 서버 등록을 가져온 후 사용자는 처음으로 연결할 때 각 서버의 암호를 입력하여 등록된 서버 목록에 암호를 저장해야 합니다. Windows 인증을 통해 등록된 서버에는 이 작업이 필요 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 등록 &#40;SQL Server Management Studio 변경 하&#41;](change-a-server-s-registration-sql-server-management-studio.md) [등록 된 서버 정보 내보내기 &#40;SQL Server Management Studio&#41;](export-registered-server-information-sql-server-management-studio.md)   
 [새 등록된 서버 만들기&#40;SQL Server Management Studio&#41;](create-a-new-registered-server-sql-server-management-studio.md)  
  
  
