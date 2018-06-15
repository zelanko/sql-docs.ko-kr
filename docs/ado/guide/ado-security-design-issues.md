---
title: ADO 보안 설계 문제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ff74ef654200dda43a951d768a505b1300bb8f4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271152"
---
# <a name="ado-security-design-features"></a>ADO 보안 디자인 기능
다음 섹션에서는 보안 디자인 기능에서 개체 ADO (ActiveX Data) 2.8 이상에 대해 설명 합니다. 보안을 개선 하기 위해 ADO 2.8에서에서 이러한 변경은 수행 했습니다. Windows Vista에서 Windows DAC 6.0에 포함 된 6.0, ADO는 ADO 2.8, Windows XP 및 Windows Server 2003에서 MDAC 2.8에 포함 된 것 같습니다. 이 항목에서는 가장 2.8 이상을 ado 응용 프로그램을 보호 하는 방법에 대 한 정보를 제공 합니다.

> [!IMPORTANT]
>  ADO의 이전 버전에서 응용 프로그램을 업데이트 하는 경우 고객에 게 배포 하기 전에 비-프로덕션 컴퓨터에 업데이트 된 응용 프로그램을 테스트 하는 것이 좋습니다. 이러한 방식으로 업데이트 된 응용 프로그램을 배포 하기 전에 호환성 문제를 알고 있는 확인할 수 있습니다.

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer 파일 액세스 시나리오
 Internet Explorer의 웹 페이지 스크립팅 하는 ADO 2.8 이상에서 사용 하는 경우의 작동 원리는 다음과 같은 기능 결과가 나타납니다.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>이제 사용자가 경고를 사용 하 여 수정 및 향상 된 보안 경고 메시지 상자
 ADO 2.7 및 이전 버전에 대 한 다음과 같은 경고 메시지가 스크립팅된 웹 페이지에서 신뢰할 수 없는 공급자에서 ADO 코드를 실행 하려고 할 때 나타납니다.

```
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 Ado 2.8 이상 위의 메시지가 더 이상 나타납니다. 대신,이 컨텍스트에서 다음과 같은 메시지가 나타납니다.

```
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 이전 메시지에는 어떤 옵션을 선택에 영향을 파악 하는 동안 합리적인된 결정을 내리려면 사용자 수 있습니다.

-   확인을 클릭 하면 모든 디스크 로부터 안전한 코드 (모든 ADO 메서드 및 속성을 제외한이 항목의 뒷부분에 설명 된 디스크에 액세스할 수 있는 Api) 허용 사용자 신뢰 사이트를 실행 하 고 브라우저 창에서를 실행 합니다.

-   사용자는 사이트를 신뢰 하지 않으면 취소를 클릭 하면 ADO 코드 실행 하 고 실행을 완전히에서 데이터 액세스를 차단 합니다.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>이제 신뢰할 수 있는 사이트를 제한 하는 디스크에 액세스할 수 있는 코드
 추가 디자인 2.8 구체적으로, 로컬 컴퓨터에 있는 파일에서 읽거나 잠재적인 노출 될 수 있는 Api의 제한 된 집합의 기능을 제한 하는 ADO에서 변경 되었습니다. 추가 된 API 메서드를 다음은 Internet Explorer를 실행 하는 경우 보안에 대 한 제한:

-   ADO에 대 한 **스트림** 경우 개체는 [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) 또는 [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) 메서드가 사용 됩니다.

-   ADO에 대 한 **레코드 집합** 경우 개체는 [저장](../../ado/reference/ado-api/save-method.md) 메서드 또는 [열려](../../ado/reference/ado-api/open-method-ado-recordset.md) 경우 처럼 메서드 중 하나는 **adCmdFile** 옵션을 설정 또는 [Microsoft OLE DB 지 속성 공급자 (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) 사용 됩니다.

 이러한 제한 된 집합 잠재적으로 디스크에 액세스할 수 있는 함수에 대 한 다음과 같은 동작이 발생 ADO 2.8 및 이후 Internet Explorer에서 이러한 메서드를 사용 하는 코드를 실행 합니다.

-   코드를 제공 하는 사이트는 신뢰할 수 있는 사이트 영역 목록에 이전에 추가 되었는지, 브라우저에서 코드를 실행 하 고 로컬 파일에 액세스 권한이 부여 됩니다.

-   사이트는 신뢰할 수 있는 사이트 영역 목록에 나타나지 않으면, 코드는 차단 되 고 로컬 파일에 대 한 액세스가 거부 되었습니다.

    > [!NOTE]
    >  ADO 2.8 이상에서 사용자 경고를 표시 하거나 사이트를 신뢰할 수 있는 사이트 영역의 목록에 추가 하는 것이 좋습니다가. 따라서 신뢰할 수 있는 사이트 목록 관리는 사용자에 게 배포 또는 로컬 파일 시스템에 액세스 해야 하는 웹 사이트-> 기반 응용 프로그램을 지원 해야 합니다.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>차단 되었습니다. 레코드 집합 개체에 대 한 ActiveCommand 속성 액세스
 2.8 ADO에 대 한 액세스 차단, Internet Explorer에서 실행할 때는 [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) 활성에 대 한 속성 **레코드 집합** 개체를 오류를 반환 합니다. 신뢰할 수 있는 사이트 목록에 등록 된 웹 사이트에서 페이지 제공 여부에 관계 없이 오류가 발생 합니다.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>OLE DB 공급자 및 통합된 보안에 대 한 처리의 변경 내용
 2.7 ADO 및 잠재적인 보안 문제 및 고려 사항에 대 한 이전 버전을 검토 하는 동안 다음과 같은 시나리오 발견 되었습니다.

 경우에 따라 통합 보안을 지 원하는 OLE DB 공급자 [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) 속성 실수로 다른 서버에 연결 하려면 ADO 연결 개체를 다시 사용 하려면 스크립트를 사용한 웹 페이지를 잠재적으로 허용할 수 사용자가 현재 로그인 자격 증명을 사용 합니다. 이 방지 하려면 ADO 2.8 및 이후 버전을 제공 하거나 제공 하지 통합된 보안에 대 한 선택한 방법에 따라 OLE DB 공급자를 처리 합니다.

 신뢰할 수 있는 사이트 영역 목록에 나열 된 사이트에서 로드 되는 웹 페이지, 다음 표에서 2.8 이상 ADO에서 각각의 경우에서 ADO 연결을 관리 하는 방법에 대 한 분석을 제공 합니다.

|사용자 인증에 대 한 IE 설정을 로그온합니다|공급자 지원 "통합 보안" 및 UID 및 PWD (SQLOLEDB) 지정|공급자는 "Integrated Security" (JOLT, 인 MSDASQL MSPersist)를 지원 하지 않습니다.|공급자는 "Integrated Security"를 지원 하며 SSPI (없음 UID/PWD 지정)로 설정 된|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|현재 사용자 이름 및 암호를 사용 하 여 자동 로그온|연결 허용|연결 허용|연결 허용|
|사용자 이름 및 암호 확인|연결 허용|연결 실패|연결 실패|
|인트라넷 영역 에서만에서 자동으로 로그온|연결 허용|사용자에 게 보안 경고|사용자에 게 보안 경고|
|익명 로그온|연결 허용|연결 실패|연결 실패|

 이제 보안 경고 표시 되는 경우 메시지 상자에는 사용자에 게 제공:

```
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 위의 메시지 보다 합리적인된 결정을 확인 하 고 상황에 따라 진행을 수 있습니다.

> [!NOTE]
>  신뢰할 수 없는 사이트 (즉, 사이트는 신뢰할 수 있는 사이트 영역 목록에 나열 되지 않은)에 대 한 사용자에 대 한 행, 안전 하지 않은 공급자에 대 한 경고 및 두 번째 경고에서 두 가지 보안 경고가 표시 될 수는 공급자도 신뢰할 수 없는 경우 (이 섹션 앞부분에서에서 설명)로,는 자신의 id를 사용 하려고 합니다. 첫 번째 경고를 확인을 클릭 하면 Internet Explorer 설정 및 앞의 표에 설명 된 응답 동작 코드가 실행 됩니다.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>ADO 연결 문자열에 암호 텍스트 반환 되는지 여부를 제어 합니다.
 값을 가져올 시도할 때는 [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) ADO에서 속성 **연결** 개체를 다음 이벤트가 발생 합니다.

1.  연결이 열려 있으면 초기화 호출 그런 다음 이루어집니다 기본 OLE DB 공급자에 연결 문자열을 가져올 수 있습니다.

2.  설정의 OLE DB 공급자에 따라는 [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) 속성, 암호는 반환 되는 다른 연결 문자열 정보에 함께 포함 합니다.

 예를 들어 경우 ADO 연결 동적 속성 **Persist Security Info** 로 설정 된 **True**, 암호 정보가 반환 되는 연결 문자열에 포함 된 합니다. 그렇지 않으면 기본 공급자 속성을 설정한 경우 **False** (예를 들어 SQLOLEDB 공급자)와 암호 정보가 반환 된 연결 문자열에서 생략 됩니다.

 공급 업체를 사용 하는 경우 (즉, 타사) ADO 응용 프로그램 코드와 함께 OLE DB 공급자에 있는지 확인 방법을 **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** 속성은 확인 하려면 구현 여부의 포함 여부 ADO 연결 문자열을 사용 하 여 암호 정보 허용 됩니다.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>로드 하 고 레코드 집합 또는 스트림을 저장 하는 경우 파일이 아닌 장치에 대 한 확인 하는 중
 Ado 2.7 및 이전 버전 파일 입/출력 작업 등 [열려](../../ado/reference/ado-api/open-method-ado-recordset.md) 및 [저장](../../ado/reference/ado-api/save-method.md) 읽기 및 쓰기 파일 기반 데이터에 따라서는 취약성 디스크가 아닌를 지정 하는 데 사용할 URL 또는 파일 이름을 사용한 파일 형식을 기반으로 합니다. 예를 들어, LPT1, COM2, PRN 합니다. TXT, AUX는 프린터와 보조 장치 간의 사용 하 여 시스템에서 특정 입/출력에 대 한 별칭으로 사용할 수 없습니다.

 Ado 2.8 이상이 기능이 업데이트 되었습니다. 열기 및 저장에 대 한 **레코드 집합** 및 **스트림** 개체, ADO 이제 URL 또는 파일 이름에 지정 된 입력 또는 출력 장치가 실제 파일 인지 확인 하는 파일 형식 검사를 수행 합니다.

> [!NOTE]
>  파일 형식 확인이 섹션에 설명 된 대로 적용 됩니다 Windows 2000 이상. 예: Windows 98 이전 Windows 릴리스의에서 ADO 2.8 이상을 실행 되 고 있는 경우에는 적용 되지 않습니다.
