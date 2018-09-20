# <a name="outlook-javascript-api-requirement-sets"></a><span data-ttu-id="1e143-101">Outlook 的 JavaScript API 要求集</span><span class="sxs-lookup"><span data-stu-id="1e143-101">Outlook JavaScript API requirement sets</span></span>

<span data-ttu-id="1e143-102">Outlook 加载项声明要求通过使用其[清单](https://docs.microsoft.com/office/dev/add-ins/develop/add-in-manifests)中的[要求](/javascript/office/manifest/requirements)元素哪些 API 版本。</span><span class="sxs-lookup"><span data-stu-id="1e143-102">Outlook add-ins declare what API versions they require by using the [Requirements](/javascript/office/manifest/requirements) element in their [manifest](https://docs.microsoft.com/office/dev/add-ins/develop/add-in-manifests).</span></span> <span data-ttu-id="1e143-103">Outlook 加载项始终包括 [Set](/javascript/office/manifest/set) 元素，其中 `Name` 属性设置为 `Mailbox` 且 `MinVersion` 属性设置为支持加载项方案的 API 最低要求集。</span><span class="sxs-lookup"><span data-stu-id="1e143-103">Outlook add-ins always include a [Set](/javascript/office/manifest/set) element with a `Name` attribute set to `Mailbox` and a `MinVersion` attribute set to the minimum API requirement set that supports the add-in's scenarios.</span></span>

<span data-ttu-id="1e143-104">例如，下面的清单段表示 1.1 的最低要求集：</span><span class="sxs-lookup"><span data-stu-id="1e143-104">For example, the following manifest snippet indicates a minimum requirement set of 1.1:</span></span>

```xml
<Requirements>
  <Sets>
    <Set Name="MailBox" MinVersion="1.1" />
  </Sets>
</Requirements>
```

<span data-ttu-id="1e143-105">所有 Outlook API 都属于 `Mailbox` [要求集](https://docs.microsoft.com/office/dev/add-ins/develop/specify-office-hosts-and-api-requirements)。</span><span class="sxs-lookup"><span data-stu-id="1e143-105">All Outlook APIs belong to the `Mailbox` [requirement set](https://docs.microsoft.com/office/dev/add-ins/develop/specify-office-hosts-and-api-requirements).</span></span> <span data-ttu-id="1e143-106">`Mailbox` 要求集具有多个版本，并且我们发布的每组新的 API 都属于更高版本的要求集。</span><span class="sxs-lookup"><span data-stu-id="1e143-106">The `Mailbox` requirement set has versions, and each new set of APIs that we release belongs to a higher version of the set.</span></span> <span data-ttu-id="1e143-107">并非所有的 Outlook 客户端都支持最新的 API 集，但如果 Outlook 客户端声明支持要求集，则它支持该要求集中的所有 API。</span><span class="sxs-lookup"><span data-stu-id="1e143-107">Not all Outlook clients support the newest set of APIs, but if an Outlook client declares support for a requirement set, it supports all of the APIs in that requirement set.</span></span>

<span data-ttu-id="1e143-p103">在清单中设置最低要求集版本可控制外接程序会显示在哪个 Outlook 客户端中。如果客户端不支持最低要求集，则不会加载外接程序。例如，如果指定要求集版本 1.3，则意味着外接程序不会显示在任何不支持 1.3 及以上版本的 Outlook 客户端中。</span><span class="sxs-lookup"><span data-stu-id="1e143-p103">Setting a minimum requirement set version in the manifest controls which Outlook client the add-in will appear in. If a client does not support the minimum requirement set, it does not load the add-in. For example, if requirement set version 1.3 is specified, this means the add-in will not show up in any Outlook client that doesn't support at least 1.3.</span></span>

## <a name="using-apis-from-later-requirement-sets"></a><span data-ttu-id="1e143-111">使用更高版本要求集中的 API</span><span class="sxs-lookup"><span data-stu-id="1e143-111">Using APIs from later requirement sets</span></span>

<span data-ttu-id="1e143-p104">设置要求集不会限制外接程序可使用的可用 API。例如，如果外接程序指定要求集 1.1，但它在支持 1.3 的 Outlook 客户端中运行，则外接程序可以使用要求集 1.3 中的 API。</span><span class="sxs-lookup"><span data-stu-id="1e143-p104">Setting a requirement set does not limit the available APIs that the add-in can use. For example, if the add-in specifies requirement set 1.1, but it is running in an Outlook client which support 1.3, the add-in can use APIs from requirement set 1.3\.</span></span>

<span data-ttu-id="1e143-114">要使用较新的 API，开发人员可使用标准 JavaScript 技术来检查是否存在新 API</span><span class="sxs-lookup"><span data-stu-id="1e143-114">To use newer APIs, developers can just check for their existence by using standard JavaScript technique</span></span>

```js
if (item.somePropertyOrFunction !== undefined) {
  item.somePropertyOrFunction ...
}
```

<span data-ttu-id="1e143-115">对于清单中所指定的要求集版本中的任何 API，无需执行此类检查。</span><span class="sxs-lookup"><span data-stu-id="1e143-115">No such checks are necessary for any APIs which are present in the requirement set version specified in in the manifest.</span></span>

## <a name="choosing-a-minimum-requirement-set"></a><span data-ttu-id="1e143-116">选择最低要求集</span><span class="sxs-lookup"><span data-stu-id="1e143-116">Choosing a minimum requirement set</span></span>

<span data-ttu-id="1e143-117">开发人员应使用包含其方案关键 API 集的最早要求集，如果不使用该要求集，外接程序将不起作用。</span><span class="sxs-lookup"><span data-stu-id="1e143-117">Developers should use the earliest requirement set that contains the critical set of APIs for their scenario, without which the add-in won't work.</span></span>

## <a name="clients"></a><span data-ttu-id="1e143-118">客户端</span><span class="sxs-lookup"><span data-stu-id="1e143-118">Clients</span></span>

<span data-ttu-id="1e143-119">下列客户端支持 Outlook 外接程序。</span><span class="sxs-lookup"><span data-stu-id="1e143-119">The following clients support Outlook add-ins.</span></span>

| <span data-ttu-id="1e143-120">客户端</span><span class="sxs-lookup"><span data-stu-id="1e143-120">Client</span></span> | <span data-ttu-id="1e143-121">受支持的 API 要求集</span><span class="sxs-lookup"><span data-stu-id="1e143-121">Supported API requirement sets</span></span> |
| --- | --- |
| <span data-ttu-id="1e143-122">Outlook 2016（即点即用）for Windows</span><span class="sxs-lookup"><span data-stu-id="1e143-122">Outlook 2016 (Click-to-Run) for Windows</span></span> | <span data-ttu-id="1e143-123">1.1、 1.2、 1.3、 1.4、 1.5、 1.6</span><span class="sxs-lookup"><span data-stu-id="1e143-123">1.1, 1.2, 1.3, 1.4, 1.5, 1.6</span></span> |
| <span data-ttu-id="1e143-124">Outlook 2016 (MSI) for Windows</span><span class="sxs-lookup"><span data-stu-id="1e143-124">Outlook 2016 (MSI) for Windows</span></span> | <span data-ttu-id="1e143-125">1.1、1.2、1.3、1.4</span><span class="sxs-lookup"><span data-stu-id="1e143-125">1.1, 1.2, 1.3, 1.4</span></span> |
| <span data-ttu-id="1e143-126">Outlook 2016 for Mac</span><span class="sxs-lookup"><span data-stu-id="1e143-126">Outlook 2016 for Mac</span></span> | <span data-ttu-id="1e143-127">1.1、 1.2、 1.3、 1.4、 1.5、 1.6</span><span class="sxs-lookup"><span data-stu-id="1e143-127">1.1, 1.2, 1.3, 1.4, 1.5, 1.6</span></span> |
| <span data-ttu-id="1e143-128">Outlook 2013 for Windows</span><span class="sxs-lookup"><span data-stu-id="1e143-128">Outlook 2013 for Windows</span></span> | <span data-ttu-id="1e143-129">1.1、1.2、1.3、1.4</span><span class="sxs-lookup"><span data-stu-id="1e143-129">1.1, 1.2, 1.3, 1.4</span></span> |
| <span data-ttu-id="1e143-130">Outlook for iPhone</span><span class="sxs-lookup"><span data-stu-id="1e143-130">Outlook for iPhone</span></span> | <span data-ttu-id="1e143-131">1.1, 1.2, 1.3, 1.4, 1.5</span><span class="sxs-lookup"><span data-stu-id="1e143-131">1.1, 1.2, 1.3, 1.4, 1.5</span></span> |
| <span data-ttu-id="1e143-132">Outlook for Android</span><span class="sxs-lookup"><span data-stu-id="1e143-132">Outlook for Android</span></span> | <span data-ttu-id="1e143-133">1.1, 1.2, 1.3, 1.4, 1.5</span><span class="sxs-lookup"><span data-stu-id="1e143-133">1.1, 1.2, 1.3, 1.4, 1.5</span></span> |
| <span data-ttu-id="1e143-134">Outlook 网页版（Office 365 和 Outlook.com）</span><span class="sxs-lookup"><span data-stu-id="1e143-134">Outlook on the web (Office 365 and Outlook.com)</span></span> | <span data-ttu-id="1e143-135">1.1、 1.2、 1.3、 1.4、 1.5、 1.6</span><span class="sxs-lookup"><span data-stu-id="1e143-135">1.1, 1.2, 1.3, 1.4, 1.5, 1.6</span></span> |
| <span data-ttu-id="1e143-136">Outlook Web App（本地 Exchange 2013）</span><span class="sxs-lookup"><span data-stu-id="1e143-136">Outlook Web App (Exchange 2013 On-Premise)</span></span> | <span data-ttu-id="1e143-137">1.1</span><span class="sxs-lookup"><span data-stu-id="1e143-137">1.1</span></span> |
| <span data-ttu-id="1e143-138">Outlook Web App（本地 Exchange 2016）</span><span class="sxs-lookup"><span data-stu-id="1e143-138">Outlook Web App (Exchange 2016 On-Premise)</span></span> | <span data-ttu-id="1e143-p105">1.1, 1.2. 1.3</span><span class="sxs-lookup"><span data-stu-id="1e143-p105">1.1, 1.2. 1.3</span></span> |

> [!NOTE] 
> <span data-ttu-id="1e143-141">在 Outlook 2013 中的 1.3 支持已添加的[年 12 月 8，2015，Outlook 2013 (KB3114349) 的更新的](https://support.microsoft.com/kb/3114349)一部分。</span><span class="sxs-lookup"><span data-stu-id="1e143-141">Support for 1.3 in Outlook 2013 was added as part of the [December 8, 2015, update for Outlook 2013 (KB3114349)](https://support.microsoft.com/kb/3114349).</span></span> <span data-ttu-id="1e143-142">在 Outlook 2013 中的 1.4 支持已添加的[年 9 月 13，2016，Outlook 2013 (KB3118280) 的更新的](https://support.microsoft.com/help/3118280)一部分。</span><span class="sxs-lookup"><span data-stu-id="1e143-142">Support for 1.4 in Outlook 2013 was added as part of the [September 13, 2016, update for Outlook 2013 (KB3118280)](https://support.microsoft.com/help/3118280).</span></span>