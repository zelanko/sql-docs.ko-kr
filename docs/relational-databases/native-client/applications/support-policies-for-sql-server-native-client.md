---
title: SQL Server Native Client에 대 한 지원 정책 Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 09c80cf4-23e6-4027-a24f-cdb9c87af811
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 400589fa583a9c75dcde2208622cff4c62e11ab9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761541"
---
# <a name="support-policies-for-sql-server-native-client"></a>SQL Server Native Client에 대한 지원 정책
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 함께 여러 데이터 액세스 구성 요소를 사용하는 방법에 대해 설명합니다.  
  
## <a name="server-support"></a>서버 지원  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0에서는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 및 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]와의 연결을 지원합니다.  
  
## <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 지원하는 운영 체제를 보여 줍니다.  
  
|SQL Server Native Client 버전|지원되는 운영 체제|  
|--------------------------------------|---------------------------------|  
|SQL Server Native Client(SQL Server 2005)|Microsoft Windows 2000 서비스 팩 4 이상<br /><br /> Microsoft Windows Server 2003 이상<br /><br /> Microsoft Windows XP 서비스 팩 1 이상<br /><br /> Microsoft Windows Vista([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 팩 2 이상 필요)<br /><br /> Microsoft Windows Server 2008 R2 (서비스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 팩 2 이상 필요)|  
|SQL Server Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])|Microsoft Windows Server 2003 서비스 팩 2 이상<br /><br /> Microsoft Windows XP 서비스 팩 2 이상<br /><br /> Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2|  
|SQL Server Native Client 10.5 ([!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)])|Microsoft Windows Server 2003 서비스 팩 2 이상<br /><br /> Microsoft Windows XP 서비스 팩 2 이상<br /><br /> Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2<br /><br /> Microsoft Windows 7|  
|SQL Server Native Client 11.0([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])|Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2<br /><br /> Microsoft Windows 7<br /><br /> Microsoft Windows 8<br /><br /> Microsoft Windows Server 2012|  
  
## <a name="ado-support-policies"></a>ADO 지원 정책  
 ADO 애플리케이션에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전의 기능이 필요하지 않은 경우 Windows에 포함된 SQLOLEDB OLE DB 공급자를 사용할 수 있습니다.  
  
 ADO 응용 프로그램에서는에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]포함 된 Native Client 버전을 사용할 수 있습니다. 또한 ADO 애플리케이션에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 포함된 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0도 사용할 수 있지만 이렇게 하려면 연결 문자열에 `DataTypeCompatibility=80`을 지정해야 합니다. 연결 문자열에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]이 있으면 `DataTypeCompatibility=80`의 기능만 사용할 수 있습니다.  
  
## <a name="bcp-support-policies"></a>BCP 지원 정책  
 
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]부터 bcp.exe에서는 bcp.exe가 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전보다 세 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전 이하인 데이터 파일을 지원합니다.  
  
## <a name="odbc-support-policies"></a>ODBC 지원 정책  
 애플리케이션은 Windows 운영 체제에 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC 드라이버를 사용해야 합니다. 애플리케이션이 특정 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 함께 사용하도록 인증된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용할 수 있습니다.  
  
## <a name="ole-db-support-policies"></a>OLE DB 지원 정책  
 애플리케이션은 Windows 운영 체제에 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 공급자를 사용해야 합니다. 용 프로그램이 특정 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 함께 사용하도록 인증된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용할 수 있습니다.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 함께 사용하도록 인증되지 않은 OLE DB 애플리케이션은 연결 문자열에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을 지정하는 경우 `DataTypeCompatibility=80` Native Client를 사용할 수 있습니다.  
  
 OLE DB Service Component를 사용하는 OLE DB 애플리케이션은 연결 문자열에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을 지정하는 경우에만 `DataTypeCompatibility=80` Native Client를 사용할 수 있습니다. 그러나이 경우에는 이후에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 추가 된 기능을 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client를 사용하여 애플리케이션 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
