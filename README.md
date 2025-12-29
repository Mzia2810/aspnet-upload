# SeymourWebsite

Professional README — detailed overview, code examples, and workflow diagram for the legacy ASP.NET Web Forms project in this repository.

**Project**
- **Name:** SeymourWebsite
- **Type:** ASP.NET Web Forms (VB.NET) web application
- **Purpose:** Membership/association website with public and private areas, SSO support, and localization.

**Features**
- **Server UI:** ASPX pages with Master pages for consistent layout.
- **Authentication:** Single Sign-On flow (SSO pages and VB code-behind).
- **Navigation:** XML-driven menus located in App_Data.
- **Localization:** Satellite resource folders under bin for multiple languages.
- **Private/Public Areas:** Content separation for authenticated members and public visitors.

**Repository layout (high level)**
- `Global.asax` — application lifecycle and error handling
- `Web.config` — configuration (authentication, connection strings, machineKey)
- `SSO.aspx` / `SSO.aspx.vb` — single sign-on implementation
- `Master.Master`, `MasterSignIn.Master` — main layouts
- `App_Data/menu.xml`, `App_Data/menuMain.xml` — menu/navigation data
- `Private/`, `Public/` — page groups
- `css/`, `Images/` — static assets

**Prerequisites**
- Windows (IIS or IIS Express)
- Visual Studio (recommended) with ASP.NET Web Forms support
- .NET Framework matching the target in `Web.config` (check the `compilation` targetFramework)

**Quick start — Run locally (Visual Studio / IIS Express)**
1. Open the solution (or folder) in Visual Studio.
2. Ensure the app pool/target framework matches the project's `Web.config`.
3. If needed, restore or place any external assemblies under the `bin/` folder.
4. Start debugging with IIS Express (F5) or run without debugging (Ctrl+F5).

Example: open and run from Visual Studio.

**Configuration**
- Review `Web.config` before running in any environment; update:
  - **Connection strings**: set production DB credentials.
  - **machineKey**: use a fixed, secure key in production to ensure auth cookie compatibility.
  - **authentication/authorization**: confirm the `authentication` mode and authorization rules for `Private/` pages.

**SSO notes & audit points**
- Inspect `SSO.aspx` and `SSO.aspx.vb` for token handling, cookie creation, and timeout logic.
- Verify that any secrets or tokens are not hard-coded and are stored/handled securely.

**Localization**
- Satellite resources and localized assemblies are present under `bin/` (de, es, ja, ru). Ensure those assemblies match the deployed app version.

**Deployment**
- Deploy as an IIS web application. Ensure:
  - The application pool runs the correct .NET Framework.
  - `Web.config` contains production-safe settings (secure connection strings, machineKey, debug=false).
  - Localization assemblies and `bin/` content are deployed.

**Security checklist (quick)**
- Do not enable `debug=true` in production `Web.config`.
- Secure `machineKey` in production.
- Restrict access to `Private/` via `Web.config` authorization rules or code checks.
- Review `SSO.aspx.vb` for cookie flags (HttpOnly, Secure) and token validation.

**Troubleshooting**
- If pages error on startup, check `Global.asax` and `PageError.aspx` for logging and stack traces.
- For missing resources, verify file permissions and the `bin/` contents on the server.

**Contributing & maintenance**
- Make incremental changes and document SSO or auth changes near `SSO.aspx.vb`.
- Keep `App_Data/menu.xml` files in sync when updating site navigation.
- Prefer small, focused pull requests with clear descriptions of functional changes.

**Contact / Next steps**
- If you want, I can:
  - Generate screenshots and an annotated architecture diagram.
  - Produce a focused security audit for authentication and `Web.config` settings.
  - Convert this README into a project wiki with pages for SSO, deployment, and developer setup.

## License

- No `LICENSE` file detected in this repository. Add one if you plan to make this project open-source.

---
_If you want, I can also: (a) generate a PNG architecture diagram from the Mermaid chart, (b) insert file-level TODO markers near `SSO.aspx.vb` and `Web.config` to guide an audit, or (c) produce a short security audit report focused on authentication._
