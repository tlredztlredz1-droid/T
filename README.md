local Content = contentContainers[""]
createToggle(afkContent, "", "", 6)

for tabName, btn in pairs(tabButtons) do
    btn.MouseButton1Click:Connect(function()
        currentTab = tabName
        for name, button in pairs(tabButtons) do button.BackgroundColor3 = (name == tabName) and COLORS.Primary or COLORS.DarkBG end
        for name, container in pairs(contentContainers) do container.Visible = (name == tabName) end
    end)
end

local menuOpen = false
iconBtn.MouseButton1Click:Connect(function()
    menuOpen = not menuOpen
    if menuOpen then
        mainFrame.Size = UDim2.new(0, 0, 0, 0)
        mainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
        mainFrame.Visible = true
        tween(mainFrame, {Size = UDim2.new(0, 260, 0, 240), Position = UDim2.new(0.5, -130, 0.5, -120)}, 0.4, Enum.EasingStyle.Back)
        notifyImportant("Menu Opened!")
    else
        tween(mainFrame, {Size = UDim2.new(0, 0, 0, 0), Position = UDim2.new(0.5, 0, 0.5, 0)}, 0.3)
        task.wait(0.3)
        mainFrame.Visible = false
    end
end)

minimizeBtn.MouseButton1Click:Connect(function()
    menuOpen = false
    tween(mainFrame, {Size = UDim2.new(0, 0, 0, 0), Position = UDim2.new(0.5, 0, 0.5, 0)}, 0.3)
    task.wait(0.3)
    mainFrame.Visible = false
end)

closeBtn.MouseButton1Click:Connect(function()
    notifyImportant("Closed!")
    tween(mainFrame, {Size = UDim2.new(0, 0, 0, 0), Position = UDim2.new(0.5, 0, 0.5, 0)}, 0.3)
        tween(iconBtn, {Size = UDim2.new(0, 0, 0, 0)}, 0.3)
    task.wait(0.4)
    for _, conn in pairs(connections) do if conn then pcall(function() conn:Disconnect() end) end end
    pcall(function() screenGui:Destroy() end)
end)
