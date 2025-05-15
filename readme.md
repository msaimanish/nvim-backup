## Running code update in init.lua

```lua
vim.keymap.set('n', '<C-M-n>', function()
  local file = vim.fn.expand('%:p')
  local ext = vim.fn.expand('%:e')
  local name = vim.fn.expand('%:t:r')
  local cmd = ''

  vim.cmd('w') -- Save file

  if ext == 'cpp' then
    cmd = 'g++ "' .. file .. '" -o "' .. name .. '" && ./"' .. name .. '"'
  elseif ext == 'py' then
    cmd = 'python3 "' .. file .. '"'
  elseif ext == 'js' then
    cmd = 'node "' .. file .. '"'
  elseif ext == 'java' then
    cmd = 'javac "' .. file .. '" && java "' .. name .. '"'
  elseif ext == 'rs' then
    cmd = 'rustc "' .. file .. '" && ./"' .. name .. '"'
  elseif ext == 'go' then
    cmd = 'go run "' .. file .. '"'
  else
    print('Unsupported filetype: ' .. ext)
    return
  end

  vim.cmd('split | terminal ' .. cmd)
end, { desc = 'Run current file based on extension' })
```

