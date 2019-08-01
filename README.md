# DailyScript
## Content
<!-- vim-markdown-toc GFM -->
* [1. FormatTable](#1. FormatTable)
* [2.](#2.)
* [3.](#3.)
* [4.](#4.)
<!-- vim-markdown-toc -->
### 1. FormatTable
```lua
function GuildPanel.FormatTable(t, tabcount)
    tabcount = tabcount or 0
    -- if tabcount > 5 then
    --     --防止栈溢出
    --     return "<table too deep>"..tostring(t)
    -- end
    local str = ""
    if type(t) == "table" then
        for k, v in pairs(t) do
            local tab = string.rep("\t", tabcount)
            if type(v) == "table" then
                str = str..tab..string.format("[%s] = {", this.FormatValue(k))..'\n'
                str = str..this.FormatTable(v, tabcount + 1)..tab..'}\n'
            else
                str = str..tab..string.format("[%s] = %s", this.FormatValue(k), this.FormatValue(v))..',\n'
            end
        end
    else
        str = str..tostring(t)..'\n'
    end
    return str
end

function GuildPanel.FormatValue(val)
    if type(val) == "string" then
        return string.format("%q", val)
    end
    return tostring(val)
end
```
