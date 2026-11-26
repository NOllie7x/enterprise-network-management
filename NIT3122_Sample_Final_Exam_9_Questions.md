# NIT3122 --- Sample Final Exam：九道题精炼复习

> 依据：`NIT3122_Answers_to_Sample_Final_Exam_Paper_S2_2022.pdf`（包含
> 2022/2021 样卷题目及参考答案）。
>
> 说明： - **Original Question** 保留样卷英文原题；Q7、Q8
> 的提示也一并保留。 - **Concise Answer**
> 将参考答案整理成适合考试书写的精炼英文。 - **中文解释**
> 用简短中文说明题目在考什么、答案为什么这样组织。 - Q1
> 的样卷参考答案主要讨论密码策略过严带来的成本，对"过松"的缺点展开不足；精炼答案补足了题干要求，并非逐字照抄参考答案。 -
> Q9
> 样卷没有提供标准答案，只说明答案取决于学生设计。下文给出一种合理示例方案，不代表唯一标准答案。

------------------------------------------------------------------------

## Q1 --- Password Policy（10 Marks）

### Original Question

> Analyse the pros and cons of enforcing too strict and not strict
> enough password policies in enterprise system.

### Concise Answer

A password policy requires a balance between security and usability.

-   **Too strict:** Users may dislike frequent password changes and may
    forget new passwords. This can increase password reset requests,
    service desk workload, organizational costs and reduce productivity.
-   **Not strict enough:** Weak passwords are easier to guess or
    compromise, increasing the risk of unauthorized access.
-   **Recommendation:** Organizations should maintain sufficient
    password security while avoiding unnecessary password changes and
    excessive user burden.

### 中文解释

题目要求比较密码策略过严和过松的影响。

过严：用户容易忘记密码，频繁找服务台重置，增加时间和金钱成本。

过松：密码容易被猜测或破解，增加未经授权访问的风险。

核心是 **Balance（平衡）**：既要保证安全，也要考虑用户体验和管理成本。

------------------------------------------------------------------------

## Q2 --- Distributed File System（DFS）（10 Marks）

### Original Question

> Provide examples and explain the advantage of using Distributed File
> System in Enterprise Network.

### Concise Answer

DFS namespaces group shared folders hosted on different servers into one
logical namespace.

For example, instead of accessing:

-   `\\FS-1\Accounting`
-   `\\FS-2\Research`
-   `\\FS-3\Management`

Users can access them through:

-   `\\contoso.com\Accounting`
-   `\\contoso.com\Research`
-   `\\contoso.com\Management`

The folders remain hosted on their original servers, but users do not
need to remember which server hosts each folder.

Advantages:

1.  **Simplified access:** Users only need to remember the shared folder
    name under one namespace.
2.  **Fault tolerance:** Shared folders can be replicated across
    servers.
3.  **Data distribution:** The same folder content can be distributed to
    multiple locations.
4.  **Closest replica:** DFS can redirect users to the closest available
    replica.

### 中文解释

DFS 把不同文件服务器上的共享文件夹组织成统一的逻辑访问路径。

-   **DFS Namespace（DFS-N）：** 解决"路径分散、不方便记忆"的问题。
-   **DFS Replication（DFS-R）：** 将共享文件夹内容复制到多个服务器。

记忆重点：**DFS-N 管统一路径，DFS-R 管文件复制。**

------------------------------------------------------------------------

## Q3 --- Fine-Grained Password Policy（FGPP）（10 Marks）

### Original Question

> A company would like to configure a separate password policy for
> members of their system administration team. The user accounts of all
> members of the system administration team are located in the
> System_Administration Organizational Unit. Provide your solution to
> address this requirement.

### Concise Answer

1.  Create a security group named `Systems_Administrators`.
2.  Add all system administrator user accounts from the
    `System_Administration` OU to this group.
3.  Create a Password Settings Object (PSO).
4.  Apply the PSO to the `Systems_Administrators` security group.

Fine-Grained Password Policies (FGPP) allow different password policies
to be applied to individual user accounts or security groups.

### 中文解释

公司希望系统管理员使用独立于普通员工的密码策略。

关键点：**FGPP 不能直接应用到 OU**，而可以应用到用户账户或安全组。

所以需要先创建安全组，把管理员账户加入组，再创建 PSO 并应用到该组。

记忆顺序：**创建安全组 → 加入管理员 → 创建 PSO → 应用 PSO。**

------------------------------------------------------------------------

## Q4 --- DNS Aging and Scavenging（10 Marks）

### Original Question

> Provide examples of configuration for Aging and Scavenging. Analyse
> the problems that may occur to the system if Aging and Scavenging is
> not configured.

### Concise Answer

Aging and Scavenging help reduce stale (out-of-date or no longer
relevant) resource records in a primary DNS zone.

**Configuration:**

1.  Enable timestamps for resource records dynamically added to primary
    zones.
2.  Age resource records based on a configured refresh time period.
3.  Enable scavenging to remove records that remain beyond the refresh
    period.

**Problems if not configured:**

1.  DNS queries may return stale records instead of relevant results.
2.  Large DNS zones may cause DNS server performance problems.
3.  Stale records may cause DNS names to point to addresses that have
    been reassigned to other devices.

### 中文解释

例如，一台旧电脑原来使用 `192.168.1.10`，退役后这个 IP 被新电脑使用，但
DNS 仍保留旧记录，就可能造成名称解析错误。

-   **Aging（老化）：** 根据时间判断记录是否陈旧。
-   **Scavenging（清理）：** 删除符合条件的陈旧记录。

不配置可能导致错误解析、DNS 区域膨胀和服务器性能问题。

------------------------------------------------------------------------

## Q5 --- DC and RODC（10 Marks）

### Original Question

> Analyse the differences between Domain Controller (DC) and Read-Only
> Domain Controller (RODC). Use examples to explain when your
> organization should consider deploying (RODC). Assume that a user
> account has not been replicated to the RODC before, analyse the
> situation when the user can and cannot sign on to the RODC.

### Concise Answer

A **Domain Controller (DC)** stores and manages Active Directory data
and supports directory changes.

A **Read-Only Domain Controller (RODC)** maintains a read-only copy of
Active Directory and stores passwords for only selected users.

**When to deploy an RODC:**

An organization should consider deploying an RODC at a branch office
where physical security is poor, such as a site without a secure, locked
server room. If the RODC is stolen, only passwords stored on that RODC
need to be considered for resetting, rather than every account password
in the domain.

**Logon scenario for an account not previously replicated to the RODC:**

-   If the RODC can connect to a writable DC, it can query the DC to
    authorize the user's logon.
-   If the connection to the writable DC is unavailable, the user cannot
    log on in this scenario because the RODC does not have the user's
    account/password information available locally.

### 中文解释

RODC 是只读域控制器，只保存部分用户的密码。

适合部署在物理安全条件较差的分支机构，降低服务器被盗后凭据泄露的影响。

题目特别强调：用户账户之前没有复制到 RODC。

因此要判断网络连接：

-   能连接可写 DC：可以向可写 DC 查询并完成认证。
-   不能连接可写 DC：由于本地没有该用户的凭据，无法完成登录。

------------------------------------------------------------------------

## Q6 --- Group Policy Processing and Enforced（10 Marks）

### Original Question

> Assume that there are multiple policies at different levels such as
> local, site, Organizational Units. Provide example and explain the
> order of how the policies are applied. What happens if you chose to
> enforce a policy?

### Concise Answer

Group Policies are normally processed in the **LSDOU** order:

1.  Local
2.  Site
3.  Domain
4.  Organizational Unit (OU)

Policies are applied from the local level to the OU level. When
conflicting settings exist, a later-applied policy normally overrides an
earlier one.

For example, if a Local GPO sets a red desktop wallpaper and an OU GPO
sets a green wallpaper, the OU setting normally takes effect.

When a GPO is configured as **Enforced**, lower-level policies cannot
override its settings. For example, an Enforced Domain GPO can override
conflicting OU-level settings.

### 中文解释

这道题考查 GPO 的应用顺序和强制策略。

记忆顺序：**LSDOU = Local → Site → Domain → OU**。

一般情况下，后应用的冲突设置覆盖先应用的设置。

但 Enforced（强制）是例外：上级被强制的 GPO 不会被下级 OU
的冲突设置覆盖。

------------------------------------------------------------------------

## Q7 --- Active Directory Object Types（10 Marks）

### Original Question

> In Lab 1, "In the Object Types dialog box, click Computers check
> box.", what's purpose of the step?

**Hint from the sample paper:**

> By default, Computer is not selected. The purpose of the step will
> allow PLABSA01 to be selected in the next step.

### Concise Answer

The purpose of selecting the **Computers** checkbox is to include
computer objects in the object selection or search results.

By default, Computer is not selected. Enabling this option allows the
administrator to find and select the computer account named `PLABSA01`
in the next step.

### 中文解释

对象选择窗口默认没有勾选 Computers。

勾选后，计算机对象就会进入搜索/选择范围，管理员才能在下一步找到并选择
`PLABSA01`。

注意：这一步只是让计算机对象可以被找到和选择，不是创建计算机账户，也不是修改其权限。

------------------------------------------------------------------------

## Q8 --- IIS and RMS（10 Marks）

### Original Question

> What a role Internet Information Services (IIS) plays in Rights
> Management Services (RMS)? Give explanation based on your experience
> with Lab 9.

**Hint from the sample paper:**

> IIS plays a crucial role in RMS implementation. It enables a web user
> access to a document and help RMS control the user's access.

### Concise Answer

IIS plays an important role in RMS implementation.

1.  IIS hosts the web services required by RMS.
2.  It allows clients, such as Microsoft Office, to communicate with RMS
    through HTTP or HTTPS.
3.  When a user requests access to a protected document, IIS receives
    the request and provides access to the RMS services.
4.  RMS checks the user's permissions and provides the appropriate
    license.

Therefore, **IIS provides the web access interface, while RMS controls
access rights to protected documents.**

### 中文解释

IIS 是 Web 服务平台，负责承载 RMS 所需的 Web
服务，为客户端提供访问入口。

RMS 则负责检查用户权限、控制受保护文档的访问。

记忆重点：**IIS 提供访问接口，RMS 管理文档权限。**

------------------------------------------------------------------------

## Q9 --- Enterprise Forest Structure and Trust Relationships（20 Marks）

### Original Question

> InfoTech has employed Window Server 2016 to implement their network.
> Their head quarter is based in Melbourne, with two departments
> Production and Sale. Production department is located in Perth while
> the Sale department is located in Sydney. Marketing department has to
> smaller departments, one is for domestic market, and one is for
> international market. InfoTech recently join with other company named
> SoftTech based in Melbourne, to expand their business.
>
> -   Design the forest structure of the enterprise network of Infotech.
>     Draw a diagram based on your design and label with appropriate
>     domain names and location of each branch and domain.
> -   Identify and explain the differences between Forest, Domain Tree
>     and Domain, Child Domains.
> -   What trust relationships can be implemented between InfoTech and
>     SoftTech? Use a diagram to explain your solution.

### Concise Answer --- One Possible Design

**1. Forest and domain structure**

Use one forest and one domain for InfoTech:

-   Forest: `infotech.com`
-   Domain: `infotech.com`
-   Melbourne: Headquarters
-   Perth: Production department
-   Sydney: Sale department
-   Marketing: Create two child OUs, `Domestic` and `International`.

Use **Organizational Units (OUs)** to organize departments and **AD
Sites** to represent the different physical locations.

Example:

``` text
Forest: infotech.com
└── Domain: infotech.com
    ├── OU: Production (Perth)
    ├── OU: Sale (Sydney)
    └── OU: Marketing (Melbourne)
        ├── OU: Domestic
        └── OU: International
```

**2. Key differences**

-   **Forest:** The highest-level Active Directory structure, which can
    contain one or more domains.
-   **Domain Tree:** A group of domains that share a contiguous DNS
    namespace.
-   **Domain:** An Active Directory administrative and security
    boundary.
-   **Child Domain:** A domain created under a parent domain, such as
    `perth.infotech.com`.

**3. Trust relationship with SoftTech**

If InfoTech and SoftTech maintain separate forests, a **Forest Trust**
can be established between them.

A two-way forest trust allows users in either forest to be authenticated
across the trust, subject to permissions on the resources being
accessed.

Example:

``` text
InfoTech Forest                 SoftTech Forest
infotech.com  <-------------->  softtech.com
                  Forest Trust
```

### 中文解释

这道题有三个任务：

1.  设计企业 AD 结构。
2.  解释 Forest、Domain Tree、Domain、Child Domain。
3.  设计 InfoTech 和 SoftTech 之间的信任关系。

一个简单合理的方案是：InfoTech 使用一个 Forest 和一个 Domain，各部门用
OU 组织，不同城市用 AD Sites 表示。Marketing 再建立 Domestic 和
International 两个子 OU。

如果 SoftTech 保留自己的独立 Forest，可以考虑建立 Forest Trust。

注意：样卷没有给出 Q9
的唯一标准答案，明确说明设计取决于学生方案。上面是一个可解释、结构简单的参考设计。

------------------------------------------------------------------------

## Final Quick Review --- 考前关键词

  -----------------------------------------------------------------------
  Question                            必须记住的关键词
  ----------------------------------- -----------------------------------
  Q1                                  Password Policy、Too Strict、Too
                                      Weak、Balance、Service Desk Cost

  Q2                                  DFS Namespace、DFS
                                      Replication、Fault
                                      Tolerance、Closest Replica

  Q3                                  FGPP、PSO、Security Group、User
                                      Accounts

  Q4                                  DNS Aging、Scavenging、Stale
                                      Records、Timestamp

  Q5                                  DC、RODC、Read-only、Physical
                                      Security、Writable DC

  Q6                                  LSDOU、GPO、Enforced、Override

  Q7                                  Object Types、Computers、PLABSA01

  Q8                                  IIS、RMS、HTTP/HTTPS、Web
                                      Services、Permissions

  Q9                                  Forest、Domain Tree、Domain、Child
                                      Domain、Forest Trust、OU、AD Sites
  -----------------------------------------------------------------------

> 复习建议：先确保每题能说出关键词，再练习用英文写出 3--5 句完整答案。Q9
> 需要额外练习画出结构图和信任关系图。
