---
title: 추적 파일에 최대 파일 크기 설정(SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- maximum file size for traces
- size [SQL Server], trace files
ms.assetid: e86dc4ce-5aa3-4c0d-acb5-c9e8871ed963
author: stevestein
ms.author: sstein
ms.openlocfilehash: fd437dec39566ae01e03df5414e29cac0c28a5d8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048299"
---
# <a name="set-a-maximum-file-size-for-a-trace-file-sql-server-profiler"></a>추적 파일에 최대 파일 크기 설정(SQL Server Profiler)
  추적 파일에 최대 파일 크기를 설정하려면 다음 절차를 수행하십시오.  
  
### <a name="to-set-a-maximum-file-size-for-a-trace-file"></a>추적 파일에 최대 파일 크기를 설정하려면  
  
1.  **파일** 메뉴에서 **새 추적**을 클릭한 다음 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결합니다.  
  
     **추적 속성**대화 상자가 표시됩니다.  
  
    > [!NOTE]  
    >  **연결한 후 즉시 추적 시작**을 선택한 경우에는 **추적 속성**대화 상자가 나타나지 않고 추적이 시작됩니다. 이 설정을 해제하려면 **도구**메뉴에서 **옵션**을 클릭한 다음 **연결한 후 즉시 추적 시작** 확인란의 선택을 취소합니다.  
  
2.  **추적 이름** 입력란에 추적의 이름을 입력합니다.  
  
3.  **템플릿 이름**목록에서 추적 템플릿을 선택합니다.  
  
4.  **파일에 저장**을 선택한 다음 추적 정보를 저장할 파일을 지정합니다.  
  
5.  **최대 파일 크기 설정** 입력란에 추적할 최대 파일 크기를 지정합니다. 파일 크기가 이 최대 크기에 도달하면 추적 이벤트는 더 이상 이 파일에 기록되지 않습니다. **파일 롤오버 사용** 을 선택하면(기본값으로 선택됨) 다음이 수행됩니다.  
  
     파일 롤오버 옵션을 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 최대 파일 크기에 도달하면 현재 파일을 닫고 새 파일을 만듭니다. 새 파일의 이름은 이전 파일의 이름과 동일하지만 이름에 순서를 나타내는 정수가 추가됩니다. 예를 들어 원래의 추적 파일 이름이 filename_1.trc라면 다음 추적 파일은 filename_2.trc입니다. 새 롤오버 파일에 할당된 이름을 기존 파일이 이미 사용했다면 읽기 전용이 아닌 경우 기존 파일을 덮어씁니다. 추적 데이터를 파일로 저장할 때 파일 롤오버 옵션이 기본적으로 사용됩니다.  
  
     파일 롤오버 옵션이 설정되어 있으면 추적은 다른 방법으로 중단되기 전까지 계속됩니다. 파일 크기 제한에 도달한 후 추적을 중지하려면 파일 롤오버 옵션을 사용하지 마십시오.  
  
    > [!NOTE]  
    >  FAT32 파일 시스템에서 파일의 크기는 4GB 미만으로 제한됩니다. 추적 파일의 크기가 이 크기에 도달하면 추적이 실패하고 "디스크 공간이 부족합니다"라는 오류 메시지가 표시됩니다. 더 큰 파일을 만들려면 NTFS 파일 시스템을 사용하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
