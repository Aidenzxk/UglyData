x <-1:1000
y <-1:1000
east <- sample(x,size = 50, replace = TRUE)
north <- sample(y, size = 50, replace = TRUE)
symbols(east, north, squares = rep(20,50),inches = FALSE)


symbols(sample(x, 40, replace = TRUE),
        sample(y, 40, replace = TRUE),
        circles = rep(25,40),
        inches = FALSE,
        fg = "green1",
        bg = "beige",
        add = TRUE)

symbols(sample(x, 12, replace = TRUE),
        sample(y, 12, replace = TRUE),
        circles = rep(35,12),
        inches = FALSE,
        fg = "green4",
        bg = "beige",
        add = TRUE)

dwellings <- cbind.data.frame(id = 1:50, east, north)




locs <- sample(1:50, 7, replace = FALSE)

lines(x = dwellings[locs, ]$east,
      y = dwellings[locs, ]$north,
      lty = 2,
      lwd = .75,
      col = "blue")

text(x = dwellings[locs, ]$east,
     y = dwellings[locs, ]$north + 3,
     labels = dwellings[locs, ]$id)

xspline(x = dwellings[locs, 2],
        y = dwellings[locs, 3],
        shape = -1,
        lty = 2)
title(main="A Person's path between Homes")
