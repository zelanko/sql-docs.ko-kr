---
title: 프로그래밍 방식으로 연결 관리자 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 973cb7dcfe7eb95e003428adf0c8a0beb7e68e87
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62877717"
---
# <a name="working-with-connection-managers-programmatically"></a>프로그래밍 방식으로 연결 관리자 사용
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 관련된 연결 관리자 클래스의 AcquireConnection 메서드는 관리 코드에서 연결 관리자를 사용할 때 가장 자주 호출하는 메서드입니다. 관리 코드를 작성할 때 연결 관리자의 기능을 사용하려면 AcquireConnection 메서드를 호출해야 합니다. 스크립트 태스크, 스크립트 구성 요소, 사용자 지정 개체 또는 사용자 지정 애플리케이션 중 어느 항목에서 관리 코드를 작성하든 관계없이 이 메서드를 호출해야 합니다.  
  
 AcquireConnection 메서드를 성공적으로 호출하려면 다음 질문에 대한 대답을 알고 있어야 합니다.  
  
-   **어떤 연결 관리자가 AcquireConnection 메서드에서 관리되는 개체를 반환합니까?**  
  
     많은 연결 관리자에서 관리되지 않는 COM 개체(System.__ComObject)를 반환하며, 이러한 개체는 관리 코드에서 사용할 수 없습니다. 이러한 연결 관리자의 목록에는 자주 사용되는 OLE DB 연결 관리자가 포함됩니다.  
  
-   **관리되는 개체를 반환하는 연결 관리자의 경우 AcquireConnection 메서드에서 반환하는 개체는 무엇입니까?**  
  
     반환 값을 적절한 형식으로 캐스팅하려면 AcquireConnection 메서드에서 반환하는 개체의 형식을 알고 있어야 합니다. 예를 들어 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자에 대한 AcquireConnection 메서드는 사용자가 SqlClient 공급자를 사용할 때 열린 SqlConnection 개체를 반환합니다. 그러나 파일 연결 관리자의 AcquireConnection 메서드는 문자열만 반환합니다.  
  
 이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에 포함된 연결 관리자에 대해 이러한 정보를 제공합니다.  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>관리되는 개체를 반환하지 않는 연결 관리자  
 다음 표에는 AcquireConnection 메서드에서 네이티브 COM 개체(System.__ComObject)를 반환하는 연결 관리자가 나열되어 있습니다. 이러한 관리되지 않는 개체는 관리 코드에서 사용하기가 어렵습니다.  
  
|연결 관리자 유형|연결 관리자 이름|  
|-----------------------------|-----------------------------|  
|ADO|ADO 연결 관리자|  
|MSOLAP90|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 연결 관리자|  
|EXCEL|Excel 연결 관리자|  
|FTP|FTP 연결 관리자|  
|HTTP|HTTP 연결 관리자|  
|ODBC|ODBC 연결 관리자|  
|OLEDB|OLE DB 연결 관리자|  
  
 일반적으로 관리 코드에서 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자를 사용하여 ADO, Excel, ODBC 또는 OLE DB 데이터 원본에 연결할 수 있습니다.  
  
## <a name="return-values-from-the-acquireconnection-method"></a>AcquireConnection 메서드의 반환 값  
 다음 표에는 AcquireConnection 메서드에서 관리되는 개체를 반환하는 연결 관리자가 나열되어 있습니다. 이러한 관리되는 개체는 관리 코드에서 쉽게 사용할 수 있습니다.  
  
|연결 관리자 유형|연결 관리자 이름|반환 값 형식|추가 정보|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|[!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자|`System.Data.SqlClient.SqlConnection`||  
|FILE|파일 연결 관리자|`System.String`|파일에 대한 경로입니다.|  
|FLATFILE|Flat File Connection Manager|`System.String`|파일에 대한 경로입니다.|  
|MSMQ|MSMQ 연결 관리자|`System.Messaging.MessageQueue`||  
|MULTIFILE|다중 파일 연결 관리자|`System.String`|파일 중 하나에 대한 경로입니다.|  
|MULTIFLATFILE|다중 플랫 파일 연결 관리자|`System.String`|파일 중 하나에 대한 경로입니다.|  
|SMOServer|SMO 연결 관리자|`Microsoft.SqlServer.Management.Smo.Server`||  
|SMTP|SMTP 연결 관리자|`System.String`|예: `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|WMI 연결 관리자|`System.Management.ManagementScope`||  
|SQLMOBILE|SQL Server Compact 연결 관리자|`System.Data.SqlServerCe.SqlCeConnection`||  
  
![Integration Services 아이콘 (작은 아이콘)](media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [스크립트 태스크에서 데이터 원본에 연결](extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [스크립트 구성 요소에서 데이터 원본에 연결](extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [사용자 지정 태스크에서 데이터 원본에 연결](extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
