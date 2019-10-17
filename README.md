# hello-world
just a learn project

GitHub, i'm coming, very excite.

static int media_neg_get_result_config(pj_pool_t *pool,
                                       od_sip_session_ctx *ctx)
{
    const pjmedia_sdp_session *active_local_sdp = 
                        ctx->session_sdp_neg.active_local_sdp;
    od_media_params *decode_param = &ctx->encode_media;
    pjmedia_sdp_conn *conn;

    conn = active_local_sdp->conn;
    if (conn != NULL) {
        /**
        * parse connection info ("c=" line), get send IP.
        */
        if (!pj_strcmp(&conn->addr_type, &STR_IP4)) {
            pj_ansi_snprintf(decode_param->conn.vid_send_ip, 
                             sizeof(decode_param->conn.vid_send_ip), 
                             "%s",
                             pj_strbuf(&conn->addr));
            
            pj_ansi_snprintf(decode_param->conn.aud_send_ip, 
                             sizeof(decode_param->conn.aud_send_ip), 
                             "%s",
                             pj_strbuf(&conn->addr));
        } else if (!pj_strcmp(&conn->addr_type, &STR_IP6)) {
            RPTERR("unsupport IPv6 yet!!!");
        } else {
            RPTERR("unknown addr_type not IPv4 or IPv6!!!");
        }
    }

    /*TODO*/

    return PJ_SUCCESS;
}
