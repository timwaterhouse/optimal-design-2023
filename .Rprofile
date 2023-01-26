mpn_date <- "2022-12-21"

mpn_url <- paste0("https://mpn.metworx.com/snapshots/stable/", mpn_date, "/")

options(
  # set repos to MPN
  repos = c(
    MPN = mpn_url,
    CRAN_Micro = "https://cran.microsoft.com/snapshot/2023-01-26",
    # a value must be set to CRAN or R will complain, so we'll point both to MPN
    CRAN = mpn_url
  ),
  # set some bbr opinionated defaults, these won't impact users who don't use bbr
  'bbr.bbi_exe_path' = file.path(getwd(), "bin", "bbi")
)

r_version <- "4.1"

correct_r <- grepl(
  paste0("R version ", r_version),
  R.version[["version.string"]],
  fixed = TRUE
)

# source after setting the repos to make sure renv will see those repo versions
if (correct_r) {
  source("renv/activate.R")
} else {
  stop(paste0("The project only works with R ", r_version))
}

if (interactive()) {

  # library info ------------------------------------------------------------
  message("repos set to: \n\t", paste0(unique(getOption('repos')), collapse = "\n\t"))
  message("library paths set to: \n\t", paste0(.libPaths(), collapse = "\n\t"))


  # bbr warnings ------------------------------------------------------------
  local({
    bbi_path <- getOption('bbr.bbi_exe_path')

    if (!file.exists(bbi_path)) {
      warning(
        sprintf("bbi not found at path `%s` ", bbi_path),
        "either run `bbr::use_bbi()` to install bbi or ",
        "check what you entered in the `bbr.bbi_exe_path` option and make sure it is correct.",
        call. = FALSE
      )
    }
  })

}

rm(mpn_date, mpn_url, r_version, correct_r)
